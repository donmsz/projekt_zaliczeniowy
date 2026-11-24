# Definition of Ready (DoR) i Definition of Done (DoD)

_Zatwierdzone przez zespół w Sprincie 0 (listopad 2026)._

## Definition of Ready (DoR)

Zadanie z Product Backlogu może wejść do Sprint Backlogu, gdy spełnia wszystkie poniższe warunki:

- [x] Opis wskazuje cel biznesowy zadania (dla historyjek użytkownika zalecany format „Jako … chcę … aby …”).
- [x] Określono jasne, weryfikowalne kryteria akceptacji (lista warunków lub format Given/When/Then).
- [x] Karta posiada priorytet MoSCoW (`Must` / `Should` / `Could`) oraz przypisaną epikę (`E1`–`E7`).
- [x] Zadanie zostało oszacowane w story points (Planning Poker, skala Fibonacciego).
- [x] Wskazano powiązanie z wymaganiem projektu (`R-xx`, `NFR-xx` lub KPI), jeśli dotyczy.
- [x] Rozmiar zadania nie przekracza **8 SP** – zadania większe (np. 13 SP) dzielimy przed rozpoczęciem sprintu.
- [x] Znane są zależności od innych zadań oraz wymagane dane wejściowe.

## Definition of Done (DoD)

Zadanie ze Sprint Backlogu może zostać przeniesione do kolumny `Done`, gdy spełnia wszystkie poniższe warunki:

- [x] Kod, diagramy lub dokumenty znajdują się w repozytorium GitHub i zostały zmergowane do `main` przez Pull Request (z numerem karty w commicie/PR).
- [x] Pull Request został sprawdzony i zaakceptowany przez co najmniej jedną inną osobę z zespołu (Code Review).
- [x] Testy (w tym testy jakości danych, jeśli dotyczą zadania) przechodzą bez błędów.
- [x] Wszystkie kryteria akceptacji zapisane na karcie Trello zostały zweryfikowane.
- [x] Dokumentacja projektowa została uzupełniona lub zaktualizowana (README, ADR, słownik danych/KPI, macierz śledzenia – jeśli dotyczy).
- [x] Przyrost jest gotowy do zademonstrowania na Sprint Review.
