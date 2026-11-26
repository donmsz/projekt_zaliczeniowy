# ADR-004: Architektura warstwowa hurtowni (staging → core → mart), RODO i odtwarzalność

- **Status:** Zaakceptowany
- **Data:** 2026-11-26
- **Autor:** Yurii Patsora
- **Powiązanie:** S01-03 (`#23`), R-01, R-02, R-03, NFR-03, NFR-05

## Kontekst

Dane EduPro pochodzą z 6 heterogenicznych źródeł (system zapisów, CRM, LMS, harmonogramowanie, ankiety, pliki finansowe) o różnej jakości, z duplikatami identyfikatorów uczestników i danymi osobowymi podlegającymi RODO (`NFR-03`). Projekt musi jednocześnie spełnić wymóg pełnej odtwarzalności środowiska przez prowadzącego w czasie poniżej 2 godzin (`NFR-05`) oraz zapewnić uzgodnienie sum finansowych ze źródłami w granicy ≤ 0,1%.

## Rozważane opcje

| Opcja | Zalety | Wady / ryzyka |
| :--- | :--- | :--- |
| **3 warstwy (`staging` → `core` → `mart`) + pseudonimizacja na wejściu do `core` (wybrana)** | Czyste rozdzielenie odpowiedzialności: `staging` przyjmuje surowe dane i pozwala audytować zgodność ze źródłem; `core` przechowuje zintegrowany, zanonimizowany model wymiarowy (SCD2 + tabela pomostowa); `mart` wystawia gotowe widoki pod KPI i Power BI. | Większa liczba obiektów SQL do utrzymania niż w pojedynczym schemacie. |
| **Jedna warstwa (bezpośrednie ładowanie do tabel raportowych)** | Szybsze uruchomienie w 1. tygodniu. | Brak śladu audytowego do uzgodnienia ze źródłami, mieszanie danych surowych z oczyszczonymi, trudniejsze wdrożenie SCD2 i RODO. |
| **Architektura Data Vault 2.0** | Bardzo wysoka elastyczność przy zmianach źródeł. | Nadmierna złożoność (Hub/Link/Satellite) nieproporcjonalna do skali projektu i czasu sprintów. |

## Decyzja

Przyjmujemy **trójwarstwową architekturę hurtowni danych w PostgreSQL**:
1. **`staging`** – surowe kopie danych ze źródeł (bez logiki biznesowej), wykorzystywane do walidacji wejścia i uzgodnień kontrolnych.
2. **`core`** – oczyszczony i zintegrowany model wymiarowy (konstelacja faktów, klucze sztuczne i biznesowe, SCD typu 2, tabela pomostowa) z **pseudonimizacją danych osobowych uczestników** (zastąpienie imienia, nazwiska i e-maila deterministycznym skrótem / kodem uczestnika zgodnie z `NFR-03`).
3. **`mart`** – widoki i tabele zagregowane zoptymalizowane pod warstwę semantyczną Power BI i wymagane KPI (w tym zagregowane wyniki quizów LMS).

Jednocześnie przyjmujemy zasadę **pełnej odtwarzalności ze źródeł w repozytorium**: wygenerowane pliki danych nie są commitowane do Git (`.gitignore`), lecz odtwarzane deterministycznie (stały `seed`) przez `src/generator/`.

## Konsekwencje

**Pozytywne:**
- Jawna separacja danych surowych od warstwy analitycznej ułatwia testowanie jakości danych (`tests/data_quality/`) i uzgodnienie finansowe (`S01-25`).
- Dane osobowe nie trafiają do warstwy `core`, `mart` ani Power BI — spełnienie wymogu RODO (`NFR-03`, `S01-26`) z poziomu architektury.
- Deterministyczny generator ze stałym `seed` gwarantuje powtarzalne wyniki u każdego członka zespołu i u prowadzącego.

**Negatywne i mitygacja:**
- Konieczność pilnowania spójności nazw kolumn między generatorem (`S01-07`), ERD (`S01-04`/`S01-05`) i skryptami SQL (`S01-08`) → weryfikacja przez obowiązkowy Pull Request i Code Review przed mergem do `main`.

## Uruchomienie przez prowadzącego

Cały przepływ (`generacja danych` → `DDL staging/core/mart` → `ETL` → `testy jakości`) jest skryptowalny i idempotentny. Przy użyciu `docker-compose.yml` i instrukcji w `README.md` odtworzenie pełnego środowiska od zera zajmie ok. 15–30 minut (znacznie poniżej limitu 2 h z `NFR-05`).
