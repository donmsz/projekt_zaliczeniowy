# Rejestr decyzji architektonicznych (ADR) – EduPro Analytics

Zadanie Trello: **S01-03 (`#23`)** | Sprint 1 | Status: do przeglądu (Code Review)

| ID | Tytuł | Status | Zakres |
| :--- | :--- | :--- | :--- |
| [ADR-001](ADR-001-hurtownia-danych-postgresql.md) | Wybór PostgreSQL jako silnika hurtowni danych | Zaakceptowany | Warstwa hurtowni (`R-01`, `R-03`, `NFR-05`) |
| [ADR-002](ADR-002-integracja-etl-python.md) | Wybór Pythona do generatora danych, ETL/ELT i testów jakości | Zaakceptowany | Warstwa integracji i DQ (`R-01`, `R-02`, `NFR-01`) |
| [ADR-003](ADR-003-narzedzie-bi-power-bi-pbip.md) | Wybór Power BI Desktop i formatu PBIP/TMDL | Zaakceptowany | Warstwa semantyczna i BI (`R-04`, `R-05`, `R-06`, `NFR-04`) |
| [ADR-004](ADR-004-architektura-warstwowa-i-odtwarzalnosc.md) | Architektura warstwowa (`staging` → `core` → `mart`), RODO i odtwarzalność | Zaakceptowany | Model, bezpieczeństwo, uruchomienie (`R-03`, `NFR-03`, `NFR-05`) |
