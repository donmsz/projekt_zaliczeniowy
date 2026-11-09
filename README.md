# EduPro Analytics

Projekt zaliczeniowy: rozwiązanie analityczne dla firmy szkoleniowej „EduPro” – od źródeł danych do dashboardów, realizowane w SCRUM z priorytetyzacją MoSCoW.

## Zespół

| Osoba | Rola | Obszary |
|---|---|---|
| _imię_ | Product Owner (zespołowy) | _uzupełnić_ |
| _imię_ | Scrum Master | _uzupełnić_ |
| _imię_ | Developer | _uzupełnić_ |
| _imię_ | Developer | _uzupełnić_ |
| _imię_ | Developer | _uzupełnić_ |

Product Owner biznesowy: prowadzący zajęcia.

## Linki

- Tablica Trello: _link_
- Opublikowane raporty: _link_

## Struktura repozytorium

```
docs/
  analysis/        mapa interesariuszy, katalog wymagań, MoSCoW, traceability
    interviews/    notatki z wywiadów i warsztatów
  architecture/    C4, ERD, data lineage, słownik danych i KPI
    adr/           rekordy decyzji architektonicznych
  scrum/           Team Agreement, DoR/DoD, metryki
    sprints/       notatki z Planning, Daily, Review, Retro (folder na sprint)
  tests/           raport z testów, uzgodnienie ze źródłem, test użyteczności
data/
  raw/             dane źródłowe (nie commitujemy dużych plików)
  generated/       wynik generatora danych syntetycznych (ignorowany)
src/
  generator/       generator danych syntetycznych
  etl/             ekstrakcja i ładowanie: sales, lms, finance, surveys
  warehouse/       DDL i transformacje: staging → core → mart
tests/
  data_quality/    reguły jakości danych (min. 10)
bi/                model BI w formie tekstowej (np. PBIP/TMDL)
```

## Uruchomienie

_Do uzupełnienia w Sprincie 1 po wyborze technologii (ADR-001). Cel: odtworzenie środowiska od zera w < 2 h (NFR-05)._

1. Wymagania wstępne: …
2. Wygenerowanie danych: …
3. Załadowanie hurtowni: …
4. Uruchomienie testów jakości: …
5. Otwarcie raportów: …

## Zasady pracy

Zobacz [CONTRIBUTING.md](CONTRIBUTING.md).
