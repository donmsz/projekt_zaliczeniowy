# Mapa interesariuszy – EduPro Analytics

## 1. Cel dokumentu
Dokument identyfikuje kluczowych interesariuszy wewnętrznych firmy szkoleniowej **EduPro**, ich cele biznesowe, główne pytania analityczne, powiązane wskaźniki KPI oraz wymagania w zakresie dostępu do danych (RODO / RLS). Identyfikatory `INT-XX` stanowią formalne źródło wymagań w Katalogu Wymagań i Macierzy Śledzenia.

---

## 2. Zestawienie interesariuszy

| ID | Rola biznesowa | Główny obszar odpowiedzialności | Priorytetowe KPI | Zakres dostępu do danych |
| :--- | :--- | :--- | :--- | :--- |
| **INT-01** | Prezes Zarządu (CEO) | Strategia, rentowność formatów i kanałów, realizacja planu | Przychód netto, liczba zapisów, marża na edycji, realizacja planu, YoY | Pełny widok zagregowany (bez danych osobowych – RODO) |
| **INT-02** | Dyrektor Sprzedaży B2B | Sprzedaż szkoleń otwartych i zamkniętych dla firm, lejek B2B | Przychód B2B, liczba przeszkolonych osób wg firmy, konwersja lejka B2B, retencja/CLV | Dane sprzedażowe B2B i lejek CRM (zmaskowane dane osobowe uczestników) |
| **INT-03** | Kierownik Produktu Szkoleniowego | Wyniki i jakość kursów w przypisanym obszarze tematycznym | Fill rate, completion rate, odsetek odwołanych edycji, marża, oceny/NPS | **RLS:** wyłącznie przypisany obszar tematyczny (np. IT, Finanse) |
| **INT-04** | Kierownik E-learningu | Efektywność kursów online (webinary i e-learning samodzielny) | Completion rate online, zaangażowanie LMS, miejsca porzuceń, ryzyko nieukończenia | Dane aktywności LMS (wyniki quizów zagregowane lub uprawniona rola) |
| **INT-05** | Kontroler Finansowy | Koszty bezpośrednie, marżowość, rabaty, zwroty, zgodność księgowa | Marża na edycji, przychód rozpoznawany w czasie, uzgodnienie ze źródłem (≤ 0,1%) | Pełne dane finansowe i kosztowe (zmaskowane dane osobowe) |
| **INT-06** | Koordynator Ośrodka Stacjonarnego | Harmonogramowanie, sale, trenerzy etatowi i zewnętrzni, frekwencja | Fill rate stacjonarny, odsetek odwołanych edycji, frekwencja, wykorzystanie sal i trenerów | Dane operacyjne edycji, sal i trenerów (**RLS** dla trenerów: tylko własne edycje) |
| **INT-07** | Kierownik Marketingu | Pozyskiwanie klientów B2C/B2B, efektywność kampanii i kanałów | Konwersja lejka B2C, CAC, ROI kampanii, retencja i CLV klienta | Dane kampanii, lejka B2C i zagregowanej sprzedaży |

---

## 3. Szczegółowa charakterystyka ról

### INT-01: Prezes Zarządu (CEO)
* **Cele biznesowe:**
  * Zwiększenie rentowności całej oferty szkoleniowej poprzez przesunięcie zasobów w stronę najbardziej dochodowych formatów (stacjonarne, online na żywo, e-learning) i obszarów tematycznych.
  * Bieżąca kontrola realizacji rocznego planu sprzedaży i dynamiki wzrostu względem poprzedniego roku (YoY).
* **Kluczowe pytania biznesowe:**
  1. Które kursy, formaty szkoleń i kanały sprzedaży (B2C vs B2B) generują najwyższy przychód netto i najwyższą marżę?
  2. Jak wyglądają bieżące wyniki firmy w porównaniu do planu sprzedaży oraz analogicznego okresu ubiegłego roku (YoY)?
  3. Jaki odsetek zaplanowanych edycji jest odwoływany i ile przychodu firma traci na nierentownych grupach?

### INT-02: Dyrektor Sprzedaży B2B
* **Cele biznesowe:**
  * Maksymalizacja przychodów ze szkoleń zamkniętych i grupowych zamówień korporacyjnych (jedno zamówienie dla wielu uczestników).
  * Zwiększenie skuteczności konwersji w lejku B2B oraz utrzymanie powracających klientów biznesowych.
* **Kluczowe pytania biznesowe:**
  1. Które firmy generują najwyższy przychód i ilu pracowników przeszkoliły w wybranym okresie?
  2. Na którym etapie lejka B2B (lead → zapytanie → oferta → zamówienie) tracimy najwięcej szans sprzedażowych?
  3. Jaki jest udział powracających klientów korporacyjnych (retencja) i jak rabaty wpływają na rentowność kontraktów B2B?

### INT-03: Kierownik Produktu Szkoleniowego (Opiekun obszaru tematycznego)
* **Cele biznesowe:**
  * Utrzymanie atrakcyjnej, rentownej oferty w zarządzanym obszarze tematycznym (np. IT, zarządzanie, finanse, języki).
  * Podnoszenie jakości szkoleń oraz dopasowanie terminów i formatów do popytu rynkowego.
* **Kluczowe pytania biznesowe:**
  1. Jakie są wyniki (zapisy, fill rate, przychód, koszty, marża) poszczególnych edycji w moim obszarze tematycznym?
  2. Które kursy i którzy trenerzy uzyskują najwyższe i najniższe oceny w ankietach ewaluacyjnych oraz NPS?
  3. Czy niższe oceny jakości korelują z niższą frekwencją lub niższym współczynnikiem ukończeń?

### INT-04: Kierownik E-learningu
* **Cele biznesowe:**
  * Podniesienie współczynnika ukończeń (completion rate) kursów online na żywo oraz asynchronicznych kursów e-learningowych bez stałej daty rozpoczęcia.
  * Szybka identyfikacja barier merytorycznych lub technicznych powodujących porzucanie nauki na platformie LMS.
* **Kluczowe pytania biznesowe:**
  1. Jaki odsetek uczestników rozpoczynających kursy online kończy je z wynikiem pozytywnym w podziale na kurs i kohortę miesiąca zapisu?
  2. Na których modułach i lekcjach w LMS najczęściej dochodzi do przerwania nauki?
  3. Jakie wzorce aktywności (logowania, czas nauki, wyniki quizów) zwiastują wysokie ryzyko nieukończenia kursu?

### INT-05: Kontroler Finansowy
* **Cele biznesowe:**
  * Pełna kontrola nad kosztami bezpośrednimi edycji (honoraria trenerów, wynajem sal, catering, materiały, licencje) oraz wpływem rabatów i zwrotów na wynik netto.
  * Zapewnienie spójności danych analitycznych z systemami źródłowymi (rozbieżność ≤ 0,1%) oraz prawidłowego rozpoznawania przychodu w czasie dla kursów wielomiesięcznych i abonamentów.
* **Kluczowe pytania biznesowe:**
  1. Jaka jest dokładna marża każdej edycji kursu po odjęciu wszystkich kategorii kosztów bezpośrednich?
  2. Jak zwroty, rezygnacje i rabaty obniżają przychód netto w poszczególnych formatach i kanałach?
  3. Jak rozkłada się przychód rozpoznawany w czasie trwania kursów wielomiesięcznych i czy sumy w hurtowni zgadzają się ze źródłem?

### INT-06: Koordynator Ośrodka Stacjonarnego
* **Cele biznesowe:**
  * Optymalne wykorzystanie sal w ośrodkach stacjonarnych (np. Warszawa, Kraków, Katowice) oraz harmonogramu trenerów etatowych i zewnętrznych.
  * Minimalizacja liczby odwoływanych edycji (brak minimum uczestników) oraz wysoka frekwencja na zajęciach.
* **Kluczowe pytania biznesowe:**
  1. Jaki jest poziom wypełnienia grup (fill rate) i frekwencji (attendance rate) w poszczególnych ośrodkach i terminach?
  2. Jak kształtuje się wykorzystanie dostępnych godzin sal oraz trenerów w relacji do kosztów ich zaangażowania?
  3. Które lokalizacje lub dni tygodnia mają najwyższy wskaźnik odwołanych edycji?

### INT-07: Kierownik Marketingu
* **Cele biznesowe:**
  * Optymalizacja budżetu marketingowego pod kątem kosztu pozyskania uczestnika (CAC) i zwrotu z kampanii (ROI).
  * Poprawa konwersji sklepu internetowego B2C oraz wzrost wartości klienta w czasie (CLV).
* **Kluczowe pytania biznesowe:**
  1. Jak wygląda konwersja w lejku B2C (wizyta → koszyk → zakup) w podziale na źródło ruchu i obszar tematyczny?
  2. Które kanały marketingowe zapewniają najniższy CAC i najwyższy ROI kampanii?
  3. Jakie kursy najczęściej generują kolejne zakupy tego samego klienta (retencja i CLV)?

---

## 4. Plan sesji wywiadów z interesariuszami
Zgodnie z wymaganiami projektu przeprowadzimy minimum 3 udokumentowane sesje wywiadów (notatki w `docs/analysis/interviews/`):
1. **Sesja 1:** Prezes Zarządu (`INT-01`) + Kontroler Finansowy (`INT-05`) – priorytety zarządcze, rentowność, marża i reguły finansowe.
2. **Sesja 2:** Kierownik Produktu (`INT-03`) + Koordynator Ośrodka (`INT-06`) – operacyjne zarządzanie edycjami, fill rate, trenerzy, RLS i jakość.
3. **Sesja 3:** Kierownik E-learningu (`INT-04`) + Dyrektor Sprzedaży B2B (`INT-02`) – porzucenia w LMS, RODO, zamówienia wieloosobowe i lejek B2B.
