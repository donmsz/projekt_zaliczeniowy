# R-03 – Modelowanie danych hurtowni EduPro

**Priorytet MoSCoW:** MUST HAVE  
**Epika:** Modelowanie danych  
**Powiązanie:** R-03

## 1. Opis modelu danych

Model hurtowni danych EduPro został zaprojektowany
w oparciu o schemat gwiazdy ze współdzielonymi
wymiarami (konstelacja faktów).

Model składa się z dwóch tabel faktów oraz sześciu
tabel wymiarów. Jego celem jest umożliwienie
wielowymiarowej analizy danych dotyczących zapisów
uczestników oraz realizacji kursów i szkoleń.

## 2. Tabele faktów i ich ziarno

| Tabela | Ziarno |
|---|---|
| Fact_Zapisy | Pojedynczy zapis uczestnika na konkretną edycję kursu. |
| Fact_Szkolenia | Pojedyncza zrealizowana edycja kursu. |

Tabela Fact_Zapisy umożliwia analizę liczby zapisów,
kwot zapisów oraz ukończenia kursów.

Tabela Fact_Szkolenia umożliwia analizę liczby
zrealizowanych szkoleń, frekwencji, czasu trwania
oraz kosztów organizacji.

## 3. Tabele wymiarów

| Tabela | Opis |
|---|---|
| Dim_Data | Informacje dotyczące daty, miesiąca, kwartału i roku. |
| Dim_Kurs | Informacje dotyczące kursów i ich kategorii. |
| Dim_Uczestnik | Informacje dotyczące uczestników kursów. |
| Dim_Prowadzacy | Informacje dotyczące prowadzących szkolenia. |
| Dim_Format | Forma realizacji kursu: online, stacjonarna lub hybrydowa. |
| Dim_Lokalizacja | Informacje dotyczące miejsca realizacji kursu. |

## 4. Relacje pomiędzy tabelami

Pomiędzy tabelami wymiarów a tabelami faktów
zastosowano relacje typu jeden do wielu (1:N)
z wykorzystaniem kluczy głównych (PK) oraz
kluczy obcych (FK).

Wymiary daty, kursu, formatu oraz lokalizacji
są współdzielone przez obie tabele faktów.

W tabeli Fact_Zapisy wymiar daty określa datę
zapisu uczestnika, natomiast w tabeli Fact_Szkolenia
datę rozpoczęcia edycji kursu.

## 5. Diagram ERD

![Diagram ERD hurtowni EduPro](EduPro_ERD.png)

Kod źródłowy modelu: [EduPro_ERD.dbml](EduPro_ERD.dbml)

## 6. Kryteria akceptacji

- [x] Model zawiera minimum 2 tabele faktów o różnym ziarnie.
- [x] Model zawiera minimum 5 wymiarów.
- [x] Uwzględniono datę, kurs i format/lokalizację.
- [x] Określono ziarno każdej tabeli faktów.
- [x] Przygotowano diagram ERD hurtowni danych.

## 7. Podsumowanie

Opracowany model hurtowni danych umożliwia analizę
popularności kursów, liczby zapisów, frekwencji
uczestników, przychodów oraz kosztów realizacji
szkoleń na różnych poziomach szczegółowości.
