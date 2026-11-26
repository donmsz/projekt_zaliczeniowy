# ADR-001: Wybór PostgreSQL jako silnika hurtowni danych

- **Status:** Zaakceptowany
- **Data:** 2026-11-26
- **Autor:** Yurii Patsora
- **Powiązanie:** S01-03 (`#23`), R-01, R-03, NFR-01, NFR-05

## Kontekst

System analityczny EduPro wymaga centralnej hurtowni danych zdolnej przechowywać minimum 24 miesiące historii sprzedaży (min. 300 edycji, min. 20 000 zapisów), dane finansowe, ankiety oraz min. 500 000 zdarzeń LMS w formacie JSON. Hurtownia musi obsługiwać schematy warstwowe (`staging`, `core`, `mart`), model wymiarowy z mechanizmem SCD typu 2 i tabelą pomostową, a jednocześnie dać się odtworzyć przez prowadzącego w czasie poniżej 2 godzin bez płatnych licencji i kont chmurowych.

## Rozważane opcje

| Opcja | Zalety | Wady / ryzyka |
| :--- | :--- | :--- |
| **PostgreSQL 16 (wybrana)** | Darmowy, open-source; natywna obsługa schematów (`staging`/`core`/`mart`), `JSONB`, indeksów, widoków zmaterializowanych i CTE; pełna zgodność z Power BI i Pythonem (`psycopg` / `SQLAlchemy`); łatwe uruchomienie w Dockerze lub lokalnie. | Wymaga poprawnego indeksowania przy większym wolumenie logów LMS (500 tys.+ wierszy). |
| **DuckDB** | Bardzo szybkie zapytania analityczne na plikach Parquet/CSV, zero konfiguracji serwera. | Słabsze natywne wsparcie bezpośredniego konektora w Power BI Desktop (wymaga sterownika ODBC); brak wielodostępowego modelu ról zbliżonego do produkcyjnego RDBMS. |
| **BigQuery / Snowflake** | Gotowa chmurowa hurtownia OLAP, skalowanie bez administracji. | Wymaga konta chmurowego, podpięcia karty / limitów free-tier i konfiguracji poświadczeń — wysokie ryzyko problemów przy odtwarzaniu projektu przez prowadzącego. |
| **SQLite** | Pojedynczy plik, brak instalacji serwera. | Brak natywnych schematów bazodanowych, ograniczone typy dat/decimal i słabsza obsługa złożonych transformacji analitycznych oraz konektora Power BI. |

## Decyzja

Wybieramy **PostgreSQL 16** jako silnik hurtowni danych EduPro Analytics, z podziałem na trzy logiczne schematy (`staging`, `core`, `mart`) w jednej bazie danych.

## Konsekwencje

**Pozytywne:**
- Pełna zgodność ze standardem SQL, łatwa implementacja SCD typu 2, tabeli pomostowej i widoków analitycznych pod Power BI.
- Natywny typ `JSONB` ułatwia przyjęcie surowych logów LMS do warstwy `staging`.
- Brak kosztów licencyjnych i zależności od zewnętrznej chmury.

**Negatywne i mitygacja:**
- Silnik wierszowy wymaga dyscypliny wydajnościowej dla faktów LMS → zastosujemy indeksy na kluczach obcych i datach oraz widoki zagregowane w warstwie `mart`.

## Uruchomienie przez prowadzącego

Baza danych zostanie dostarczona z plikiem `docker-compose.yml` (oficjalny obraz `postgres:16`) oraz skryptami DDL w `src/warehouse/`. Prowadzący uruchomi gotową instancję jednym poleceniem (`docker compose up -d`) lub na lokalnej instalacji PostgreSQL 16, bez zakładania zewnętrznych kont.
