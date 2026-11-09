# Zasady pracy z repozytorium

Prowadzący ocenia wkład indywidualny m.in. na podstawie historii repozytorium i tablicy zadań, więc każda zmiana musi być powiązana z kartą na Trello.

## Gałęzie

- `main` – zawsze działająca wersja; bez bezpośrednich commitów.
- Gałąź na zadanie: `<typ>/<nr-karty>-<krótki-opis>`, np. `feat/23-fakt-zapisow`, `fix/31-duplikaty-uczestnikow`, `docs/12-adr-platforma`.

## Commity

Format: `<typ>(<obszar>): <opis> [#<nr-karty>]`

- typy: `feat`, `fix`, `docs`, `test`, `refactor`, `chore`
- obszary: `etl`, `dwh`, `bi`, `gen`, `dq`, `docs`, `scrum`

Przykład: `feat(dwh): tabela fakt_zapis z ziarnem 1 zapis [#23]`

## Pull requesty

- Każdy PR przegląda co najmniej 1 inna osoba (wymóg Definition of Done).
- W opisie PR link do karty Trello i krótka informacja, jak przetestowano zmianę.
- Merge dopiero po zielonych testach jakości danych.

## Czego nie commitujemy

Haseł, kluczy, plików `.env`, dużych plików z danymi (wynik generatora odtwarzamy skryptem) ani danych osobowych.
