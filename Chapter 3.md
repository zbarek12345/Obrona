# Normalizacja Bazy Danych 
Normalizacja bazy danych to proces prowadzący do sprowadzenia tabel do stanu uporządkowanego 


w ramach normalizacji bazy rozróżnia się następujące 3 stopnie, oraz kolejne 3 pojawiające się jedynie w literaturze, będące jednak rzadziej stosowane w biznesie i praktycznych zastosowaniu.

[1NF](#pierwsza-postać-normalna-1nfzasady-1nf)  
[2NF](#druga-postać-normalna-2nf)  
[3NF](#trzecia-postać-normalna-3nf)

## Pierwsza postać normalna (1NF)
### Zasady 1NF:
- Każda kolumna zawiera tylko atomowe (niepodzielne) wartości
(nie ma wielowartościowych pól, list, tablic, zagnieżdżonych rekordów itp.)
- Nie ma grup powtarzających się kolumn
(np. telefon1, telefon2, telefon3, email1, email2 itd.)
- Każdy wiersz jest unikalny
(najczęściej osiągane przez istnienie klucza głównego – primary key)
- Kolumna → wartość jest relacją 1:1
(jedna komórka = dokładnie jedna, konkretna wartość)
### Przykład
Przed normalizacją tabela przykładowa wygląda następująco:
| id |  imię |         telefony         |        adresy_email        |        ulubione_kolory       |
|:--:|:-----:|:------------------------:|:--------------------------:|:----------------------------:|
| 1  | Anna  | 501 222 333, 602 444 555 | anna@wp.pl, anna@gmail.com | czerwony, niebieski, zielony |
| 2  | Marek | 789 123 456              | marek@o2.pl                | niebieski                    |


W tej tabeli pojawiły się następujące błędy normalizacji: 
- telefony → wiele wartości w jednej komórce
- adresy_email → wiele wartości w jednej komórce
- ulubione_kolory → lista w jednej komórce

Po normalizacji zaś uzyskamy 4 różne tabele, gwarantujące atomowość itd.

``` [text]
Tabela: osoby
+----+-------+
| id | imię  |
+----+-------+
| 1  | Anna  |
| 2  | Marek |
+----+-------+

Tabela: telefony_osób
+------------+-------------+
| osoba_id   | numer       |
+------------+-------------+
| 1          | 501222333   |
| 1          | 602444555   |
| 2          | 789123456   |
+------------+-------------+

Tabela: emaile_osób
+------------+------------------+
| osoba_id   | email            |
+------------+------------------+
| 1          | anna@wp.pl       |
| 1          | anna@gmail.com   |
| 2          | marek@o2.pl      |
+------------+------------------+

Tabela: ulubione_kolory_osób
+------------+---------------+
| osoba_id   | kolor         |
+------------+---------------+
| 1          | czerwony      |
| 1          | niebieski     |
| 1          | zielony       |
| 2          | niebieski     |
+------------+---------------+
```

__Tabela jest w pierwszej postaci normalnej, gdy każda komórka przechowuje dokładnie jedną, niepodzielną wartość, a nie listy, zbiory ani powtarzające się kolumny.__

## Druga postać normalna (2NF)

Druga postać normalna (2NF) dotyczy tabel, które już są w [1NF](#pierwsza-postać-normalna-1nf) i dodatkowo spełniają warunek:
Żadna kolumna niebędąca kluczem głównym nie zależy tylko od części klucza głównego
(inaczej mówiąc: eliminujemy częściowe zależności – partial dependencies)

## Klasyczny przykład biznesowy – zamówienia i produkty
__Tabela, która jest w [1NF](#pierwsza-postać-normalna-1nf), ale NIE jest w 2NF__

Produkty
| id_zamówienia | id_produktu | nazwa_produktu | cena_katalogowa | ilosc |
|---------------|-------------|----------------|-----------------|-------|
| 1001          | P001        | iPhone 14      | 4199.00         | 2     |
| 1001          | P005        | Etui silikon   | 149.00          | 1     |
| 1002          | P001        | iPhone 14      | 4199.00         | 1     |
| 1003          | P007        | Ładowarka 20W  | 129.00          | 3     |

Następnie podzielimy ją na 2 odrębne tabele, dzięki czemu nie będzie powtórzeń.
Tabela Produkty

| id_produktu | nazwa               | cena_katalogowa |
|-------------|---------------------|-----------------|
| P001        | iPhone 14           | 4199.00         |
| P005        | Etui silikonowe     | 149.00          |
| P007        | Ładowarka 20W USB-C | 129.00          |

Tabela Pozycje_zamówienia

| id_zamówienia | id_produktu | ilosc |
|---------------|-------------|-------|
| 1001          | P001        | 2     |
| 1001          | P005        | 1     |
| 1002          | P001        | 1     |
| 1003          | P007        | 3     |

Szybkie porównanie – co zyskujemy przechodząc do 2NF

|             Aspekt            |        Przed 2NF (jedna tabela)        |            Po 2NF (dwie tabele)           |
|:-----------------------------:|:--------------------------------------:|:-----------------------------------------:|
| Zmiana nazwy produktu         | trzeba zmienić we wszystkich wierszach | wystarczy zmienić 1 raz w tabeli Produkty |
| Zmiana ceny katalogowej       | to samo – wiele miejsc                 | 1 miejsce                                 |
| Miejsce na dysku              | dużo duplikacji                        | znacznie mniej                            |
| Ryzyko niekonsekwencji danych | bardzo duże                            | praktycznie wyeliminowane                 |
| Łatwość utrzymania            | niska                                  | wysoka                                    |

Krótka reguła-pamiątka:
Jeśli masz klucz złożony → sprawdź, czy wszystkie kolumny nie-kluczowe zależą od całego klucza, a nie tylko od jego części.

## Trzecia postać normalna (3NF)
Tabela jest w 3NF, jeżeli jest w [2NF](#druga-postać-normalna-2nf) i nie zawiera przechodnich zależności (tranzytatywnych zależności),
czyli żadna kolumna nie-kluczowa nie zależy od innej kolumny nie-kluczowej.

Faktury
| id_faktury | id_klienta | nazwa_klienta     | nip_klienta   | miasto_klienta | ulica_klienta       | data_wystawienia | id_produktu | nazwa_produktu   | cena_netto |
|------------|------------|-------------------|---------------|----------------|---------------------|------------------|-------------|------------------|------------|
| FV/2026/001| K001       | TechSolutions Sp.z o.o. | 5252468112 | Warszawa       | ul. Prosta 12/3     | 2026-01-05       | P001        | Laptop Pro X     | 4599.00    |
| FV/2026/001| K001       | TechSolutions Sp.z o.o. | 5252468112 | Warszawa       | ul. Prosta 12/3     | 2026-01-05       | P007        | Mysz bezprzewodowa | 89.00    |
| FV/2026/002| K015       | Nowa Era Edu      | 6340101123 | Kraków         | Rynek 5             | 2026-01-08       | P001        | Laptop Pro X     | 4599.00    |

- nazwa_klienta → zależy od id_klienta
- nip_klienta → zależy od id_klienta
- miasto_klienta → zależy od id_klienta
- ulica_klienta → zależy od id_klienta

Wszystkie te informacje zależą od id_klienta, a nie bezpośrednio od klucza głównego faktury → klasyczna przechodnia zależność.

Po przeniesieniu na 3F uzyskamy następujące tabele: 
1. Klienci

| id_klienta | nazwa_klienta           | nip_klienta   | miasto     | ulica              |
|------------|-------------------------|---------------|------------|--------------------|
| K001       | TechSolutions Sp.z o.o. | 5252468112    | Warszawa   | ul. Prosta 12/3    |
| K015       | Nowa Era Edu            | 6340101123    | Kraków     | Rynek 5            |

2. Faktury (nagłówek)

| id_faktury | id_klienta | data_wystawienia |
|------------|------------|------------------|
| FV/2026/001| K001       | 2026-01-05       |
| FV/2026/002| K015       | 2026-01-08       |

3. Pozycje_faktur

| id_faktury | lp_pozycji | id_produktu | nazwa_produktu      | ilosc | cena_netto |
|------------|------------|-------------|---------------------|-------|------------|
| FV/2026/001| 1          | P001        | Laptop Pro X        | 1     | 4599.00    |
| FV/2026/001| 2          | P007        | Mysz bezprzewodowa  | 3     | 89.00      |
| FV/2026/002| 1          | P001        | Laptop Pro X        | 2     | 4599.00    |

To samo dotyczy nazwy przedmiotu i jego ceny ale zignorujmy to na razie (Załóżmy że to backup na wypadek jakby sprzedawca kasował nie istniejące encje z tabeli produkty).

|             Problem / operacja             |      Przed 3NF (jedna/duża tabela)     |        Po 3NF (trzy tabele)        |
|:------------------------------------------:|:--------------------------------------:|:----------------------------------:|
| Zmiana adresu klienta                      | trzeba zmienić we wszystkich fakturach | 1 zmiana w tabeli Klienci          |
| Dodanie nowego klienta bez faktury         | niemożliwe lub trzeba wpisać śmieci    | normalna operacja                  |
| Miejsce na dysku (dużo faktur)             | bardzo dużo duplikacji                 | wielokrotnie mniej                 |
| Ryzyko niekonsekwentnych danych adresowych | bardzo wysokie                         | praktycznie zerowe                 |
| Łatwość raportowania „klienci z Warszawy”  | trzeba parsować wszystkie wiersze      | proste zapytanie po tabeli Klienci |


## Postać BCNF 
Każdy determinant w tabeli musi być kluczem kandydatem.
Innymi słowy:
Jeśli A → B (A wyznacza B), to A musi być kluczem superkluczem (czyli zawierać jakiś klucz kandydacki).

### Przykład 
Grafik_pokoi
| id_pokoju | dzień_tygodnia | godzina_początku | specjalizacja | lekarz_nazwisko | nr_licencji |
|-----------|----------------|------------------|---------------|-----------------|-------------|
| P-12      | Poniedziałek   | 08:00            | Kardiologia   | Nowak           | PL-45678    |
| P-12      | Poniedziałek   | 11:00            | Kardiologia   | Nowak           | PL-45678    |
| P-12      | Wtorek         | 08:00            | Endokrynologia| Malinowski      | PL-91234    |
| P-15      | Poniedziałek   | 08:00            | Neurologia    | Kowalski        | PL-56789    |

Klucze kandydackie:

{id_pokoju, dzień_tygodnia, godzina_początku}  
{lekarz_nazwisko, dzień_tygodnia, godzina_początku}   ← drugi, mniej oczywisty

Zależności funkcyjne:

id_pokoju, dzień_tygodnia, godzina_początku → specjalizacja, lekarz_nazwisko, nr_licencji  
__lekarz_nazwisko → specjalizacja, nr_licencji__     ← problem!

lekarz_nazwisko __nie jest__ kluczem kandydackim,
ale jest __determinantem → naruszenie BCNF__ 
(determinuje licencję lekarza (Błąd w tej tabeli jest jednocześnie naruszeniem 3NF))

### Wersja poprawiona

1. Lekarze

| lekarz_nazwisko | specjalizacja   | nr_licencji  |
|-----------------|-----------------|--------------|
| Nowak           | Kardiologia     | PL-45678     |
| Malinowski      | Endokrynologia  | PL-91234     |
| Kowalski        | Neurologia      | PL-56789     |

2. Grafik (główny)

| id_pokoju | dzień_tygodnia | godzina_początku | lekarz_nazwisko |
|-----------|----------------|------------------|-----------------|
| P-12      | Poniedziałek   | 08:00            | Nowak           |
| P-12      | Poniedziałek   | 11:00            | Nowak           |
| P-12      | Wtorek         | 08:00            | Malinowski      |
| P-15      | Poniedziałek   | 08:00            | Kowalski        |

3. Pokoje (opcjonalnie – jeśli chcemy mieć dodatkowe informacje o pokojach)


| id_pokoju | piętro | budynek | powierzchnia_m² |
|-----------|--------|---------|-----------------|
| P-12      | 1      | A       | 18              |
| P-15      | 2      | A       | 22              |

|              Sytuacja / operacja              |          3NF (jedna tabela)         |             BCNF (rozbite)             |
|:---------------------------------------------:|:-----------------------------------:|:--------------------------------------:|
| Zmiana specjalizacji lekarza                  | trzeba zmienić wiele wierszy        | 1 miejsce – tabela Lekarze             |
| Dodanie nowego lekarza bez grafiku            | niemożliwe lub trzeba wpisać NULL-e | normalna operacja                      |
| Anomalia wstawiania (nowy lekarz bez grafiku) | występuje                           | wyeliminowana                          |
| Anomalia usuwania (ostatni grafik lekarza)    | usuwasz specjalizację i licencję    | nie ma problemu                        |
| Złożoność zapytań                             | prostsze                            | nieco bardziej złożone (więcej joinów) |

### Drugi przykład BCNF

| Student      | Kurs       | Nauczyciel     |
|--------------|------------|----------------|
| Jan Kowalski | Matematyka | Prof. Iksiński |
| Anna Nowak   | Matematyka | Prof. Iksiński |
| Jan Kowalski | Fizyka     | Dr Ygrekowski  |
| Tomek Zając  | Matematyka | Mgr Wiśniewski |
| Maria Kot    | Matematyka | Mgr Wiśniewski |

Dlaczego jest to problem (Dlaczego to nie jest BCNF?)? 

Klucz kandydujący A: {Student, Kurs} (Znając studenta i kurs, wiemy kto go uczy).

Klucz kandydujący B: {Student, Nauczyciel} (Znając studenta i nauczyciela, wiemy na jaki kurs chodzi, bo nauczyciel uczy tylko jednego).

__Problem__: Spójrzmy na kolumny Nauczyciel i Kurs. Widzimy zależność: Prof. Iksiński → Matematyka.  
Informacja "Prof. Iksiński uczy Matematyki" jest powtórzona w wierszu 1 i 2. Nauczyciel jest determinantą (decyduje o kursie), ale nie jest kluczem (sam "Prof. Iksiński" nie identyfikuje unikalnie wiersza, bo uczy wielu studentów).

Rozwiązanie:

Tabela __Nauczyciel_Kurs__
| Nauczyciel (PK) | Kurs       |
|-----------------|------------|
| Prof. Iksiński  | Matematyka |
| Dr Ygrekowski   | Fizyka     |
| Mgr Wiśniewski  | Matematyka |
| Prof. Zet       | Historia   |
| Maria Kot       | Matematyka |

Tabela __Student_Nauczyciel__
| Student (PK) | Nauczyciel (PK, FK) |
|--------------|---------------------|
| Jan Kowalski | Prof. Iksiński      |
| Anna Nowak   | Prof. Iksiński      |
| Jan Kowalski | Dr Ygrekowski       |
| Tomek Zając  | Mgr Wiśniewski      |
| Maria Kot    | Mgr Wiśniewski      |


Kiedy najczęściej spotykamy problem BCNF w praktyce?

Tabele typu „osoba → zespół → kierownik zespołu”  
„pokój → dzień → godzina → lekarz → specjalizacja”  
„projekt → faza → osoba odpowiedzialna za fazę”  
„samochód → kierowca → kategoria prawa jazdy”  
„klient → oddział → region / kierownik oddziału”  

### Bardzo praktyczna reguła-pamiątka:
Jeśli w tabeli jest więcej niż jeden sensowny sposób na jej unikalne zidentyfikowanie (więcej niż jeden klucz kandydacki)
→ prawie zawsze warto sprawdzić, czy nie ma naruszenia BCNF.

# Czwarta postać normalna (4NF)
rozwiązuje problem wielowartościowych zależności (multi-valued dependencies, MVD),
które mogą występować nawet w tabelach będących w BCNF.  

## Kiedy tabela jest w 4NF?
Tabela jest w 4NF wtedy i tylko wtedy, gdy każda nietrywialna wielowartościowa zależność
jest konsekwencją klucza kandydata (czyli w praktyce – gdy nie ma „niezależnych” grup wielokrotnych faktów w tej samej tabeli).  

__Najprostsza intuicja__:
Jeśli jeden wiersz reprezentuje niezależne kombinacje dwóch (lub więcej) zbiorów wartości,
to najprawdopodobniej powinniśmy to rozbić na osobne tabele.
### Klasyczny, bardzo czytelny przykład biznesowy
__Sytuacja__:
Firma prowadzi szkolenia.
Każdy trener może prowadzić wiele tematów.
Każdy trener może współpracować z wieloma firmami-kontrahentami.

| id_trenera | imię_trenera | temat_szkolenia          | firma_kontrahent     |
|------------|--------------|---------------------------|-----------------------|
| T001       | Anna Malinowska | SQL Zaawansowany         | ABC Tech Sp. z o.o.   |
| T001       | Anna Malinowska | SQL Zaawansowany         | Nowe Rozwiązania SA   |
| T001       | Anna Malinowska | Power BI od podstaw      | ABC Tech Sp. z o.o.   |
| T001       | Anna Malinowska | Power BI od podstaw      | MegaKorp Sp. z o.o.   |
| T002       | Marek Nowak     | Python dla analityków    | FuturSoft             |
| T002       | Marek Nowak     | Python dla analityków    | DataVision            |

To klasyczna wielowartościowa zależność (MVD):  
id_trenera →→ temat_szkolenia  
id_trenera →→ firma_kontrahent

### Rozwiązanie
1. Trenerzy
   
| id_trenera | imię_trenera    |
|------------|-----------------|
| T001       | Anna Malinowska |
| T002       | Marek Nowak     |

2. Trener_Tematy

| id_trenera | temat_szkolenia          |
|------------|---------------------------|
| T001       | SQL Zaawansowany         |
| T001       | Power BI od podstaw      |
| T001       | Azure Data Factory       |
| T002       | Python dla analityków    |

3. Trener_Kontrahenci

| id_trenera | firma_kontrahent       |
|------------|-------------------------|
| T001       | ABC Tech Sp. z o.o.     |
| T001       | Nowe Rozwiązania SA     |
| T001       | MegaKorp Sp. z o.o.     |
| T002       | FuturSoft               |
| T002       | DataVision              |

|                  Operacja / problem                  |         Przed 4NF (jedna tabela)        |      Po 4NF (trzy tabele)     |
|:----------------------------------------------------:|:---------------------------------------:|:-----------------------------:|
| Dodanie nowego tematu przez trenera                  | trzeba dodać wiersze dla każdej firmy   | 1 wiersz w Trener_Tematy      |
| Dodanie nowego kontrahenta dla trenera               | trzeba dodać wiersze dla każdego tematu | 1 wiersz w Trener_Kontrahenci |
| Anomalia wstawiania (nowy temat bez kontrahenta)     | występuje                               | wyeliminowana                 |
| Anomalia usuwania (ostatni temat danego kontrahenta) | usuwasz też informację o kontrahencie   | brak problemu                 |
| Rozmiar bazy przy dużej liczbie tematów i firm       | ogromna redundancja (kartezjańska)      | liniowy wzrost                |
| Łatwość zmiany nazwy tematu                          | wiele miejsc                            | jedno miejsce                 |

# Piąta postać normalna (5NF)
Piąta postać normalna jest ostatnim „klasycznym” poziomem normalizacji i rozwiązuje bardzo specyficzny problem:
Nie można wiarygodnie odtworzyć oryginalnej tabeli
poprzez złączenie (join) jej projekcji,
jeśli oryginalna tabela zawierała informacje o cyklicznych/zależnych kombinacjach trzech lub więcej atrybutów.

## Klasyczny przykład biznesowy – Zaopatrzenie / Dostawcy / Części / Projekty

__Sytuacja biznesowa__:
Firma produkcyjna korzysta z wielu dostawców.
Każdy dostawca dostarcza określone części.
Każdy projekt wymaga określonych części.
Istnieje reguła biznesowa:
„Jeśli dany dostawca dostarcza daną część i dany projekt wymaga danej części,
to ten dostawca może dostarczać tę część na ten projekt”.

Dostawy_części_projekty     ← tabela NIE w 5NF
| dostawca   | część     | projekt   |
|------------|-----------|-----------|
| D1         | C100      | P01       |
| D1         | C100      | P02       |
| D1         | C200      | P01       |
| D2         | C100      | P02       |
| D2         | C300      | P03       |

### Zależności (reguły biznesowe):

Dostawca dostarcza część:  
D1 → C100, C200  
D2 → C100, C300  

Projekt wymaga części:  
P01 → C100, C200  
P02 → C100  
P03 → C300  

### Rozwiązanie: 
1. Dostawca_Część

| dostawca   | część     |
|------------|-----------|
| D1         | C100      |
| D1         | C200      |
| D2         | C100      |
| D2         | C300      |

2. Część_Projekt

| część     | projekt   |
|-----------|-----------|
| C100      | P01       |
| C100      | P02       |
| C200      | P01       |
| C300      | P03       |

3. Dostawca_Projekt   (opcjonalna, ale często potrzebna w praktyce)

| dostawca   | projekt   |
|------------|-----------|
| D1         | P01       |
| D1         | P02       |
| D2         | P02       |
| D2         | P03       |

Po rozbiciu na te trzy tabele:

- Możemy swobodnie dodawać/usuwać fakty o tym kto co dostarcza, co jest potrzebne w projekcie i kto z kim współpracuje  
- Oryginalna tabela (Dostawca, Część, Projekt) jest odtworzeniem (joinem) tych trzech tabel  
- Nie ma już anomalii aktualizacji przy zmianie któregokolwiek z tych trzech rodzajów faktów

|                     Sytuacja                    | Czy 4NF wystarczy? | Czy potrzebna 5NF? |                  Przyczyna                  |
|:-----------------------------------------------:|:------------------:|:------------------:|:-------------------------------------------:|
| Trener – tematy – kontrahenci                   | Tak                | Nie                | dwie niezależne wielowartościowe zależności |
| Dostawca – część – projekt (z regułą cykliczną) | Tak                | Tak                | cykliczna zależność trzech predykatów       |
| Pracownik – umiejętność – projekt               | Często tak         | Często tak         | bardzo częsty realny przypadek w IT         |
| Lekarz – specjalizacja – oddział                | Zazwyczaj nie      | Czasami tak        | zależy od reguł biznesowych                 |
| Produkt – cecha – rynek docelowy                | Często tak         | Bardzo często tak  | klasyczny przypadek e-commerce/B2B          |

Większość firm zatrzymuje się na 3NF/BCNF.  
4NF robi się w 15–25% bardziej złożonych modeli.  
5NF naprawdę wprowadza się głównie tam, gdzie występują bardzo kosztowne błędy biznesowe przy aktualizacji cyklicznych zależności (branże: produkcja, IT projekty, logistyka, lotnictwo, automotive).  
Chcesz zobaczyć porównanie rozmiaru bazy i liczby wierszy przy 4NF vs 5NF na większym zbiorze danych?