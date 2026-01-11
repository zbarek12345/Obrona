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

Następnie podzielimy ją na 3 odrębne tabele, dzięki czemu nie będzie powtórzeń.
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