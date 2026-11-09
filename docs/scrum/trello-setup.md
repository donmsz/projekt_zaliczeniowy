# Konfiguracja tablicy Trello

## Listy (od lewej)

1. **Product Backlog** – wszystkie historyjki, posortowane wg priorytetu.
2. **Ready** – historyjki spełniające Definition of Ready.
3. **Sprint Backlog** – wybrane na bieżący sprint; pierwsza karta to „Cel sprintu: …”.
4. **In Progress**
5. **Code Review**
6. **Done (sprint N)** – po zakończeniu sprintu archiwizujemy karty lub przenosimy listę.
7. **Won't have** – świadomie wyłączone z zakresu, z uzasadnieniem w opisie.

## Etykiety

- MoSCoW: `Must` (czerwona), `Should` (pomarańczowa), `Could` (żółta), `Won't` (szara).
- Epiki (osobne kolory): `E1 Analiza`, `E2 Architektura`, `E3 Dane i ETL`, `E4 Hurtownia`, `E5 KPI i raporty`, `E6 Jakość danych`, `E7 Proces SCRUM`.
- Sprint: `S0` … `S5`.

## Pola niestandardowe (Custom Fields)

- `SP` – liczba (story points).
- `Wymaganie` – tekst (np. FR-04, NFR-02).
- `Sprint` – lista wyboru (S0–S5).

## Power-Upy

- **GitHub** – podpinanie commitów i PR do kart.
- Custom Fields (jeśli nie są dostępne w planie, SP wpisujemy w tytule: `[3] Fakt zapisów`).

## Szablon karty historyjki

```
Jako <rola> chcę <funkcja>, aby <cel>.

Kryteria akceptacji:
- Given … When … Then …
- Given … When … Then …

Wymaganie: FR-xx
```

## Metryki

Trello nie rysuje burndown ani velocity – prowadzimy je w arkuszu `docs/scrum/metrics` (dzienny stan pozostałych SP, SP planowane vs zrealizowane na sprint, historyjki przeniesione z powodem).

## Dostęp

Dodać prowadzącego do tablicy jako obserwatora/członka.
