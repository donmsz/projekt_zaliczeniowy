# ADR-002: Wybór Python 3 do generatora danych, procesów ETL/ELT i testów jakości

- **Status:** Zaakceptowany
- **Data:** 2026-11-26
- **Autor:** Yurii Patsora
- **Powiązanie:** S01-03 (`#23`), R-01, R-02, NFR-01, NFR-04, NFR-05

## Kontekst

Projekt wymaga zbudowania spójnego generatora danych syntetycznych w różnych formatach (CSV, XLSX, JSON — w tym ≥ 500 000 zdarzeń LMS), procesów ekstrakcji, czyszczenia, deduplikacji uczestników i ładowania danych do PostgreSQL oraz minimum 10 automatycznych testów jakości danych. Rozwiązanie musi być w całości wersjonowane w Git (kod tekstowy) i uruchamialne na dowolnym systemie operacyjnym (Windows/Linux/macOS).

## Rozważane opcje

| Opcja | Zalety | Wady / ryzyka |
| :--- | :--- | :--- |
| **Python 3 + SQL (wybrana)** | Jeden wspólny stos dla generatora (`src/generator/`), ETL (`src/etl/`) i testów jakości (`tests/data_quality/`); bogaty ekosystem (`pandas`, `faker`, `openpyxl`, `psycopg`/`SQLAlchemy`, `pytest`); łatwe przetwarzanie JSON/CSV/XLSX i wersjonowanie w Git; wysokie kompetencje zespołu. | Wymaga pilnowania struktury projektu, logowania i obsługi błędów (brak gotowego GUI orkiestratora w bazowej wersji). |
| **dbt Core + Python (generator osobno)** | Świetne zarządzanie transformacjami SQL, testami i lineage wewnątrz hurtowni. | Nadal wymaga Pythona do generatora i warstwy Extract-Load; dodatkowa warstwa konfiguracji wydłużająca wdrożenie w Sprincie 1. |
| **Apache Airflow / Prefect** | Dojrzała orkiestracja harmonogramów i retry. | Zbyt ciężka infrastruktura jak na środowisko zaliczeniowe (utrudnia odtworzenie < 2 h na maszynie prowadzącego). |
| **Talend / Pentaho (GUI ETL)** | Wizualne projektowanie przepływów. | Pliki XML trudne do Code Review w Git, ciężka instalacja lokalna (JVM/klient desktop). |

## Decyzja

Wybieramy **Python 3 (3.11+)** jako główną technologię dla generatora danych syntetycznych, modułów ekstrakcji/ładowania (`src/etl/`) oraz testów jakości danych (`tests/data_quality/`), łącząc go z transformacjami **SQL** wykonywanymi bezpośrednio w PostgreSQL (podejście ELT dla warstw `staging` → `core` → `mart`).

## Konsekwencje

**Pozytywne:**
- Jednolity stos technologiczny zmniejsza próg wejścia dla wszystkich 5 członków zespołu.
- Pełna czytelność diffów w Pull Requestach na GitHubie (`NFR-04`).
- Generowanie i ładowanie 500 000 zdarzeń LMS można zoptymalizować paczkami (`COPY` w PostgreSQL), skracając czas pełnego przeładowania do kilku minut.

**Negatywne i mitygacja:**
- Brak wbudowanego harmonogramu → w Sprincie 1 uruchomienie odbywa się przez skrypt główny CLI; automatyzacja i monitoring błędów są zaplanowane jako osobne zadanie `Should` (`S01-35`).

## Uruchomienie przez prowadzącego

Zależności zostaną utrwalone w `requirements.txt` (środowisko `.venv`). Prowadzący odtworzy dane i zasilenie hurtowni sekwencją 3 prostych poleceń (`pip install -r requirements.txt`, uruchomienie generatora, uruchomienie ETL i testów `pytest`), bez instalowania ciężkich platform orkiestracyjnych.
