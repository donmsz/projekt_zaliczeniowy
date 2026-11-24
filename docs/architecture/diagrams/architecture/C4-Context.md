C4 – Context: system analityczny EduPro
Zadanie: S01-01  
Sprint: 1  
Epika: Architektura rozwiązania  
Priorytet: Must have  
Status architektury: projekt do uzgodnienia z zespołem
Cel i zakres
Diagram kontekstowy przedstawia system analityczny EduPro jako jedną całość, jego użytkowników biznesowych oraz zewnętrzne źródła danych. System wspiera analizę sprzedaży, realizacji szkoleń, efektywności nauki, jakości i rentowności. Diagram przedstawia docelowy kontekst, a nie stan wdrożenia w Sprincie 1.
Diagram C4 Context
```mermaid
C4Context
    title System analityczny EduPro – diagram kontekstowy
    Person(board, "Zarząd", "Analizuje wyniki i podejmuje decyzje")
    Person(sales, "Dyrektor sprzedaży B2B", "Analizuje sprzedaż firmową")
    Person(product, "Kierownik produktu", "Monitoruje wyniki kursów i edycji")
    Person(center, "Koordynator ośrodka", "Analizuje frekwencję i wykorzystanie zasobów")
    Person(learning, "Kierownik e-learningu", "Analizuje postępy i ukończenia")
    Person(finance, "Kontroler finansowy", "Analizuje koszty i rentowność")
    Person(marketing, "Specjalista ds. marketingu", "Analizuje kanały pozyskania klientów")
    System(edupro, "System analityczny EduPro", "Integruje dane i udostępnia wskaźniki oraz raporty biznesowe")
    System_Ext(reg, "System zapisów i sprzedaży", "Zapisy, zamówienia, płatności i zwroty")
    System_Ext(crm, "CRM", "Klienci indywidualni i firmowi, lejek sprzedaży")
    System_Ext(lms, "Platforma LMS", "Aktywność, postępy, quizy i ukończenia")
    System_Ext(schedule, "System harmonogramowania", "Terminy, sale i trenerzy")
    System_Ext(survey, "Narzędzie ankiet ewaluacyjnych", "Oceny i odpowiedzi uczestników")
    System_Ext(cost, "Źródło danych finansowych", "Pliki kosztowe szkoleń i marketingu")
    Rel(board, edupro, "Korzysta z dashboardu zarządczego")
    Rel(sales, edupro, "Analizuje sprzedaż B2B")
    Rel(product, edupro, "Analizuje wyniki edycji")
    Rel(center, edupro, "Analizuje realizację szkoleń")
    Rel(learning, edupro, "Analizuje efektywność nauki")
    Rel(finance, edupro, "Analizuje koszty i marżę")
    Rel(marketing, edupro, "Analizuje kanały sprzedaży")
    Rel(edupro, reg, "Pobiera dane sprzedażowe")
    Rel(edupro, crm, "Pobiera dane klientów")
    Rel(edupro, lms, "Pobiera zdarzenia edukacyjne")
    Rel(edupro, schedule, "Pobiera dane harmonogramów")
    Rel(edupro, survey, "Pobiera wyniki ankiet")
    Rel(edupro, cost, "Importuje dane kosztowe")
    UpdateLayoutConfig($c4ShapeInRow="4", $c4BoundaryInRow="1")
```
Interpretacja
Użytkownicy korzystają z raportów systemu analitycznego; strzałki wskazują kierunek relacji korzystania.
System analityczny pobiera dane z systemów zewnętrznych; strzałki opisują zależność pobierania, a nie fizyczny kierunek przepływu danych.
Dane finansowe są reprezentowane jako zewnętrzne źródło plikowe, bez zakładania istnienia konkretnej aplikacji finansowej.
PostgreSQL, Python i Power BI zostaną przedstawione na poziomie C4 Container.
Analityka marketingowa oraz pozostałe funkcje Should/Could są elementami docelowej wizji, zależnymi od zakresu uzgodnionego z PO.
Powiązanie z wymaganiami
Dokument „Projekt zaliczeniowy: rozwiązanie analityczne dla firmy szkoleniowej – lista wymagań”, rozdziały 1, 4, 5, 6 i 10. Diagram wspiera projektowanie realizacji R-01 (integracja źródeł), R-05 (dashboard zarządczy), R-06 (raport operacyjny) oraz pozostałych analiz. Sam diagram nie stanowi implementacji tych wymagań.
Weryfikacja kryteriów akceptacji
Kryterium	Sposób weryfikacji
System analityczny EduPro	Widoczny centralny element System
Najważniejsze role użytkowników	Siedem elementów Person, do uzgodnienia z mapą interesariuszy
Powiązania ze sprzedażą, LMS i finansami	Elementy System_Ext oraz opisane relacje
Zapis w dokumentacji projektu	Umieszczenie tego pliku w repozytorium i sprawdzenie renderowania diagramu na GitHubie
Decyzje i ograniczenia
Nazwy ról i źródeł przyjęto na podstawie scenariusza projektowego; należy je porównać z ustaleniami Sprintu 0. Nie określono jeszcze protokołów integracji ani szczegółów implementacyjnych. Przed zamknięciem zadania należy wykonać przegląd diagramu zgodnie z zespołową Definition of Done.
