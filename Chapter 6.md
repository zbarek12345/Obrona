# Język UML w projektowaniu oprogramowania.
UML (Unified Modeling Language), czyli Znormalizowany Język Modelowania, to standardowy język wizualny służący do specyfikowania, wizualizowania i dokumentowania systemów informatycznych. Nie jest językiem programowania, lecz narzędziem, które pozwala „narysować” architekturę programu przed napisaniem kodu.

## 1. Zastosowania UML: Gdzie i po co?
UML stosuje się wszędzie tam, gdzie system jest zbyt złożony, by opisać go samym tekstem.

- Komunikacja: Służy jako wspólny język dla programistów, analityków biznesowych i klientów.

- Projektowanie architektury: Pozwala zaplanować strukturę klas, baz danych i interakcji między modułami.

- Dokumentacja: Stanowi trwały zapis tego, jak system ma działać, co ułatwia wdrażanie nowych pracowników.

- Inżynieria w przód i wstecz: Niektóre narzędzia potrafią generować szkielet kodu (np. w Javie czy C++) na podstawie diagramów UML lub odwrotnie.

## 2. Typy diagramów UML
UML 2.5 dzieli diagramy na dwie główne kategorie: Strukturalne i Behawioralne.

### A. Diagramy Strukturalne (Statyczne)
Opisują, z jakich części składa się system.

- Diagram Klas (Class Diagram): Najważniejszy w programowaniu obiektowym. Pokazuje klasy, ich atrybuty, metody oraz powiązania między nimi.

- Diagram Obiektów: Przedstawia instancje klas w konkretnym punkcie w czasie (konkretne dane).

- Diagram Komponentów: Opisuje fizyczny podział systemu na moduły, biblioteki i pliki.

- Diagram Wdrożenia (Deployment Diagram): Pokazuje fizyczną infrastrukturę (serwery, chmura, urządzenia).

### B. Diagramy Behawioralne (Dynamiczne)
Opisują, jak system zachowuje się w czasie.

- Diagram Przypadków Użycia (Use Case Diagram): Pokazuje interakcje między użytkownikami (aktorami) a systemem. Odpowiada na pytanie: "Co system robi?", a nie "Jak?".

- Diagram Sekwencji (Sequence Diagram): Skupia się na przepływie komunikatów między obiektami w czasie (kolejność zdarzeń). Kluczowy przy projektowaniu API.

- Diagram Maszyny Stanów (State Machine): Opisuje cykl życia obiektu (np. zamówienie: Nowe -> Opłacone -> Wysłane).

- Diagram Aktywności: Przypomina schemat blokowy; pokazuje logikę biznesową i algorytmy.

## 3. Relacje w UML
Relacje to "linie", które łączą elementy na diagramach. Ich precyzyjne zrozumienie jest kluczowe:
| Relacja       | Opis                                                                                         | Symbol                              |
|---------------|----------------------------------------------------------------------------------------------|-------------------------------------|
| Asocjacja     | Zwykłe powiązanie między klasami (np. Pracownik – Biuro).                                    | Linia ciągła                        |
| Agregacja     | Relacja "całość-część", gdzie części mogą istnieć bez całości (np. Klasa – Uczeń).           | Linia z pustym rombem               |
| Kompozycja    | Silna relacja "całość-część" – jeśli usuniemy całość, części też giną (np. Budynek – Pokój). | Linia z pełnym rombem               |
| Dziedziczenie | Klasa pochodna przejmuje cechy klasy bazowej.                                                | Linia z pustą strzałką              |
| Realizacja    | Implementacja interfejsu przez klasę.                                                        | Linia przerywana z pustą strzałką   |
| Zależność     | Chwilowe użycie jednej klasy przez drugą (zmiana w jednej może wpłynąć na drugą).            | Linia przerywana ze zwykłą strzałką |


## 4. Dokładne opisy każdego (ważnego dla nas) diagramu

### Diagram klas
Diagram Klas to najważniejszy i najczęściej stosowany diagram strukturalny w języku UML. Służy do przedstawienia statycznej struktury systemu poprzez opisanie klas, ich atrybutów, metod (operacji) oraz wzajemnych powiązań.

Można go porównać do planu architektonicznego, który pokazuje, jak zbudowane są poszczególne „cegiełki” (klasy) oprogramowania.

### 1. Budowa Klasy na Diagramie
Każda klasa jest reprezentowana przez prostokąt podzielony na trzy poziome sekcje:

__Nazwa klasy__: Znajduje się na górze (zwykle pogrubiona). Jeśli nazwa jest pisana kursywą, oznacza to klasę abstrakcyjną.

__Atrybuty (Właściwości)__: Środkowa sekcja. Opisuje dane, które przechowuje obiekt.

__Operacje (Metody)__: Dolna sekcja. Opisuje zachowania, czyli co obiekt potrafi zrobić.

__Modyfikatory dostępu (Widoczność)__
Przed nazwami atrybutów i metod stosuje się symbole określające ich dostępność:

$+$ Public (publiczny): Dostępny dla wszystkich.

$-$ Private (prywatny): Dostępny tylko dla danej klasy.

\# Protected (chroniony): Dostępny dla klasy i jej dzieci (dziedziczenie).

\~ Package (pakietowy): Dostępny dla klas w tym samym pakiecie.

__Przykład zapisu:__
```
- cena: Decimal;
+ obliczRabat(procent: Int): Decimal;
```

## 2. Relacje między klasami
To kluczowy element diagramu, który pokazuje, jak obiekty współpracują.

#### A. Dziedziczenie (Generalizacja)
Wskazuje, że klasa pochodna przejmuje cechy klasy bazowej.

Symbol: Linia ciągła zakończona pustym grotem strzałki skierowanym do klasy nadrzędnej.

Przykład: "Samochód" dziedziczy po klasie "Pojazd".

#### B. Asocjacja
Zwykłe powiązanie między klasami. Może mieć określoną liczebność (krotność):

1 – dokładnie jeden.

0..* – zero lub wiele.

1..* – jeden lub wiele.

Przykład: "Pracownik" jest przypisany do "Biura".

#### C. Agregacja i Kompozycja (Całość – Część)
Dwa rodzaje relacji, w których jedna klasa zawiera drugą:

1. __Agregacja (słaba)__: Część może istnieć bez całości.   
__Symbol__: pusty romb. (np. Uniwersytet i Profesor – jeśli uczelnia zniknie, profesor nadal istnieje).

2. __Kompozycja (silna)__: Część nie może istnieć bez całości.  
__Symbol__: zamalowany (czarny) romb. (np. Książka i Strony – jeśli zniszczymy książkę, strony przestają istnieć jako integralny byt).

### 3. Przykład praktyczny: System Sklepu
Wyobraźmy sobie prosty system:

__Klasa Klient__ ma asocjację 1 do 0..* z klasą Zamówienie.

__Klasa Zamówienie__ składa się z Pozycji Zamówienia (Kompozycja – bez zamówienia pozycja nie ma sensu).

__Klasa Produkt__ jest powiązana z Pozycją Zamówienia.

### 4. Kiedy stosować diagram klas?
__Podczas analizy__: Aby zrozumieć pojęcia biznesowe (model dziedziny).

__Podczas projektowania__: Aby zaplanować strukturę kodu i interfejsy przed implementacją.

__Podczas dokumentacji__: Aby pokazać innym programistom, jak moduły systemu są ze sobą połączone.

## Czym jest diagram obiektów w UML?

Diagram obiektów UML reprezentuje konkretną instancję diagramu klas w określonym momencie. Gdy przedstawimy go wizualnie, zobaczysz wiele podobieństw do diagramu klas.

Diagram obiektów koncentruje się na atrybutach zbioru obiektów i na tym, jak te obiekty są ze sobą powiązane. Na przykład na poniższym schemacie obiektu wszystkie trzy konta bankowe są powiązane z bankiem. Tytuły klas przedstawiają rodzaje kont (oszczędnościowe, rozliczeniowe i karty kredytowe), jakie dany klient może mieć w tym konkretnym banku. Atrybuty klasy są różne w przypadku poszczególnych typów kont. Na przykład karta kredytowa ma limit kredytowy, a konta oszczędnościowe i rozliczeniowe są oprocentowane. Aby lepiej zapoznać się z tym dokumentem, kliknij tutaj.

Diagramy obiektów mogą być wykorzystywane zarówno w bankowości, jak i w innych dziedzinach, ponieważ z łatwością możesz stworzyć diagram obiektów na potrzeby drzew genealogicznych, działów korporacji lub dowolnego innego systemu z powiązanymi ze sobą elementami.

![Diagram Obiektów](https://d2slcw3kip6qmk.cloudfront.net/marketing/pages/chart/what-is-an-object-diagram-in-UML/Object-Diagram-Example-4-750x400@2x.png)

### Elementy diagramu obiektów
__Obiekty__  
Obiekty są instancjami klas. Na przykład, jeśli „samochód” jest klasą, to Nissan Altima z 2007 roku jest obiektem tej klasy.

__Tytuły klas__  
Tytuły klas to charakterystyczne atrybuty danej klasy. Na diagramie obiektu drzewa genealogicznego tytuły klas zawierają imię, płeć i wiek członków rodziny. Tytuły klas możesz umieszczać jako elementy na obiekcie, a nawet we właściwościach samego obiektu (np. kolor).

![Diagram Obiektów 2 ](https://d2slcw3kip6qmk.cloudfront.net/marketing/pages/chart/UML-object-diagram-tutorial/Object_Diagram.PNG)

__Atrybuty klasy__
Atrybuty klasy są przedstawione za pomocą prostokąta z dwoma wypustkami, który wskazuje na element oprogramowania.

__Łącza__
Łącza to linie, które łączą ze sobą dwa kształty diagramu obiektów. Poniższy schemat obiektu korporacyjnego przedstawia, jak połączone są działy w tradycyjnym schemacie organizacyjnym.

### Zastosowania schematów obiektów
Diagramy obiektów przydadzą się deweloperowi w wielu przypadkach. Należą do nich:
- Badanie konkretnej iteracji systemu ogólnego.
- Przegląd systemu, który chcesz rozwijać.
- Testowanie diagramu klas, który został stworzony na potrzeby przedstawienia ogólnej struktury systemu, z wykorzystaniem diagramów obiektów dla konkretnych przypadków użycia.

## Diagram Wdrożenia
To jedyny diagram UML, który skupia się na sprzęcie. Pokazuje, na jakich fizycznych urządzeniach (węzłach) zainstalowane są poszczególne części oprogramowania.

__Zastosowanie__: Planowanie infrastruktury sieciowej, konfiguracja serwerów, rozmieszczenie mikroserwisów.

__Elementy__: "Węzły" (Nody) rysowane jako bryły (sześciany), które reprezentują serwery, laptopy czy urządzenia mobilne.

![Diagram Wdrożenia](https://wolski.pro/wp-content/uploads/2024/07/diagramy_uml_diagram_wdrozenia_polaczenia_fiziczne.png)

## 4. Diagram Struktur Złożonych
Opisuje wewnętrzną strukturę klasy lub komponentu. Pokazuje, jak mniejsze części współpracują wewnątrz "czarnej skrzynki", aby zrealizować konkretne zadanie.

__Zastosowanie__: Projektowanie bardzo złożonych obiektów, które składają się z wielu mniejszych, współpracujących ze sobą elementów.

| Perspektywa          | Sugerowany Diagram  |
|----------------------|---------------------|
| Logika i kod         | Diagram Klas        |
| Przykładowe dane     | Diagram Obiektów    |
| Moduły i biblioteki  | Diagram Komponentów |
| Serwery i sieć       | Diagram Wdrożenia   |
| Organizacja projektu | Diagram Pakietów    |

![Diagram Strultur](https://sparxsystems.com/images/screenshots/uml2_tutorial/CP01.GIF)
![Diagram Strultur 2](https://i.sstatic.net/WipGa.gif)

## 5. Diagram Pakietów (Package Diagram) 
Służy do organizowania elementów modelu w grupy (pakiety). Przypomina to układanie plików w folderach na komputerze.

Zastosowanie: Zarządzanie dużą dokumentacją i pokazywanie zależności między całymi warstwami systemu (np. warstwa logiki biznesowej vs warstwa bazy danych).

Symbol: Kształt przypominający zakładkę w segregatorze.  
![Diagram Pakietów](https://online.visual-paradigm.com/repository/images/88031adf-45b4-4587-baf8-0a4b2af2f702/package-diagram-design/uml-package-diagram-example-general-business-system.png)


## 