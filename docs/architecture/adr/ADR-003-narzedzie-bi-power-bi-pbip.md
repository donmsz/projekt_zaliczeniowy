# ADR-003: Wybór Power BI Desktop i formatu PBIP/TMDL dla warstwy BI

- **Status:** Zaakceptowany
- **Data:** 2026-11-26
- **Autor:** Yurii Patsora
- **Powiązanie:** S01-03 (`#23`), R-04, R-05, R-06, NFR-04, NFR-05

## Kontekst

EduPro potrzebuje warstwy semantycznej ze spójnymi definicjami KPI (przychód netto, fill rate, completion rate, marża na edycji, YoY, plan sprzedaży), interaktywnego dashboardu zarządczego, raportu operacyjnego oraz wsparcia dla Row-Level Security (RLS). Jednocześnie wymaganie `NFR-04` wymusza wersjonowanie modelu BI i raportów w repozytorium Git z możliwością przeprowadzania Code Review.

## Rozważane opcje

| Opcja | Zalety | Wady / ryzyka |
| :--- | :--- | :--- |
| **Power BI Desktop + format PBIP/TMDL (wybrana)** | Standard rynkowy BI; bogaty język miar DAX (time intelligence YoY, marże, kohorty); natywne RLS; darmowy Power BI Desktop do otwierania lokalnego; format `PBIP/TMDL` zapisuje model i raport jako pliki tekstowe (Git-friendly). | Działa natywnie na Windows; publikacja online w Power BI Service wymaga konta organizacyjnego/uczelnianego. |
| **Power BI Desktop + plik `.pbix`** | Najprostszy zapis w jednym pliku. | Format binarny — brak sensownych diffów w Git, częste konflikty przy pracy zespołowej (wykluczony w `.gitignore`). |
| **Apache Superset / Metabase** | Działają w przeglądarce (Docker, cross-platform), open-source. | Słabsza warstwa semantyczna (brak odpowiednika DAX), mniejsze możliwości interaktywnego projektowania dashboardów zarządczych i RLS w wersji darmowej. |
| **Looker Studio** | Darmowe narzędzie webowe. | Zależność od dostępu publicznego do bazy lub ręcznego wrzucania plików, ograniczone modelowanie wielofaktowe i brak lokalnego wersjonowania w Git. |

## Decyzja

Wybieramy **Power BI Desktop** jako narzędzie warstwy semantycznej i raportowej oraz **Power BI Project (`PBIP` z definicją modelu w `TMDL`)** jako obowiązkowy format zapisu artefaktów BI w katalogu `bi/`. Pliki binarne `.pbix` i lokalny cache są wyłączone z repozytorium w `.gitignore`.

## Konsekwencje

**Pozytywne:**
- Miary DAX, relacje schematu gwiazdy i reguły RLS są zapisane w czytelnych plikach tekstowych — można je przeglądać w Pull Requestach (`NFR-04`).
- Bezpośrednie połączenie Power BI z PostgreSQL (warstwa `mart`) zapewnia spójność danych z hurtownią.
- Power BI Desktop jest bezpłatny, więc prowadzący może otworzyć projekt `bi/*.pbip` lokalnie bez wykupywania licencji.

**Negatywne i mitygacja:**
- Power BI Desktop wymaga systemu Windows → na wypadek pracy lub odbioru na macOS/Linux do repozytorium dołączymy także eksporty PDF/zrzuty ekranu raportów oraz instrukcję połączenia z lokalną bazą PostgreSQL.

## Uruchomienie przez prowadzącego

Po uruchomieniu bazy PostgreSQL i załadowaniu danych prowadzący otwiera plik `.pbip` z katalogu `bi/` w bezpłatnym **Power BI Desktop**, wskazuje lokalne połączenie PostgreSQL (`localhost:5432`) i klika **Odśwież** (Refresh).
