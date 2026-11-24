# EduPro Analytics

Projekt zaliczeniowy: rozwiązanie analityczne dla firmy szkoleniowej **EduPro** – od źródeł danych do dashboardów biznesowych, realizowane w metodyce SCRUM z priorytetyzacją MoSCoW.

## Zespół (Grupa 2)

| Osoba | Rola w SCRUM | Obszary techniczne (min. 2) |
| :--- | :--- | :--- |
| **Kamil Zbylut** | Product Owner | Backlog i MoSCoW, architektura (C4), analiza BI i KPI |
| **Michał Szymański** | Scrum Master | Proces SCRUM i metryki, architektura danych, SQL/hurtownia |
| **Yurii Patsora** | Developer | Architektura i ADR, analiza wymagań, konfiguracja repo/Trello, wsparcie i Code Review |
| **Filip Pocentek** | Developer | Modelowanie hurtowni danych (ERD, SCD2), SQL, testy danych |
| **Jan Rojewski** | Developer | Python, generator danych i ETL, raportowanie BI |

## Linki

- **Tablica Trello:** [https://trello.com/b/BKMZIot8/edupro-analytics](https://trello.com/b/BKMZIot8/edupro-analytics)
- **Opublikowane raporty (Power BI):** _do uzupełnienia w Sprincie 2_
- **Arkusz metryk SCRUM:** _do uzupełnienia (link do arkusza Burndown / Burnup / Velocity)_

## Stos technologiczny (Sprint 1)

- **Integracja i generator danych:** Python 3 (skrypty ETL/ELT)
- **Hurtownia danych:** PostgreSQL (warstwy `staging` → `core` → `mart`)
- **Warstwa semantyczna i raportowanie:** Power BI Desktop (projekt `PBIP` / `TMDL`)

Szczegółowe uzasadnienie decyzji znajduje się w `docs/architecture/adr/` (zadanie `S01-03`).

## Struktura repozytorium

    docs/
      analysis/        mapa interesariuszy, katalog wymagań, MoSCoW, traceability
        interviews/    notatki z wywiadów i warsztatów
      architecture/    słownik danych i KPI
        adr/           rekordy decyzji architektonicznych (min. 4 ADR)
        diagrams/      diagramy C4 (Context, Container), ERD, Data Lineage
      scrum/           Team Agreement, DoR/DoD, konfiguracja Trello, metryki
        sprints/       notatki z Planning, Daily, Review, Retro (folder na sprint)
      tests/           raport z testów jakości, uzgodnienie ze źródłem, test użyteczności
    data/
      raw/             dane źródłowe (pliki wygenerowane lokalnie, wyłączone z Git)
      generated/       wynik generatora danych syntetycznych (wyłączony z Git)
    src/
      generator/       generator danych syntetycznych (min. 24 mies., 500 tys. zdarzeń LMS)
      etl/             ekstrakcja i ładowanie: sales, lms, finance, surveys
      warehouse/       DDL i transformacje: staging → core → mart
    tests/
      data_quality/    reguły i testy jakości danych (min. 10)
    bi/                model i raporty Power BI w formacie tekstowym (PBIP/TMDL)

## Uruchomienie

_Instrukcja odtworzenia środowiska od zera w czasie < 2 h (NFR-05) zostanie uzupełniona w Sprincie 1 po zakończeniu zadań `S01-07` i `S01-08`._

1. Wymagania wstępne: Python 3.11+, PostgreSQL 16 (lub Docker), Power BI Desktop.
2. Wygenerowanie danych syntetycznych: `src/generator/` _(w przygotowaniu)_.
3. Utworzenie struktur i załadowanie hurtowni: `src/warehouse/` + `src/etl/` _(w przygotowaniu)_.
4. Uruchomienie testów jakości danych: `tests/data_quality/` _(w przygotowaniu)_.
5. Otwarcie raportów: projekt Power BI z katalogu `bi/` _(w przygotowaniu)_.

## Zasady pracy

Zobacz [CONTRIBUTING.md](CONTRIBUTING.md), [Team Agreement](docs/scrum/team-agreement.md) oraz [DoR i DoD](docs/scrum/dor-dod.md).
