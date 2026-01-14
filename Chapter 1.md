# Paradygmaty programowania obiektowego (OOP)

Programowanie obiektowe (ang. Object-Oriented Programming, OOP) jest jednym z najpopularniejszych paradygmatów programowania. Polega na modelowaniu rzeczywistości za pomocą **obiektów**, które są instancjami **klas**. Klasa definiuje szablon zawierający **atrybuty** (dane, stan) oraz **metody** (zachowania, operacje na danych). Obiekty komunikują się ze sobą poprzez wysyłanie wiadomości (wywoływanie metod).

OOP pozwala na lepsze odwzorowanie świata rzeczywistego, ułatwia utrzymanie kodu w dużych projektach oraz promuje ponowne użycie kodu. Podstawowe koncepcje wywodzą się z języka Simula (1967), a popularyzację przyniósł Smalltalk w latach 70.

#### Główne filary (zasady) programowania obiektowego

Większość źródeł wyróżnia cztery fundamentalne zasady OOP:

1.  **Abstrakcja** Polega na ukryciu złożonych szczegółów implementacji i eksponowaniu tylko niezbędnego interfejsu. Programista pracuje z uproszczonym modelem obiektu, bez potrzeby znajomości jego wewnętrznego działania. _Przykład_: Klasa Samochód może mieć metodę jedź(), która ukrywa szczegóły silnika, skrzyni biegów itp.
2.  **Hermetyzacja (enkapsulacja)** Dane i metody są zamknięte w obiekcie, a dostęp do danych jest kontrolowany (np. poprzez modyfikatory dostępu: private, public). Chroni to stan obiektu przed nieautoryzowanymi zmianami. _Przykład_: Atrybuty klasy są prywatne, a dostęp do nich zapewniają publiczne metody getter/setter.
3.  **Dziedziczenie** Pozwala na tworzenie nowych klas na podstawie istniejących (klasa potomna dziedziczy atrybuty i metody klasy bazowej). Promuje hierarchię i ponowne użycie kodu. _Przykład_: Klasa SportowySamochód dziedziczy po Samochód i dodaje nowe metody, np. turbo().
4.  **Polimorfizm** Obiekty różnych klas mogą być traktowane jednolicie (np. poprzez interfejsy lub klasy bazowe). Pozwala na wywoływanie tej samej metody w różny sposób w zależności od obiektu. _Przykład_: Metoda rysuj() w klasach Koło, Kwadrat – każda implementuje ją inaczej, ale można wywołać na liście figur.

Te cztery zasady umożliwiają tworzenie modularnego, skalowalnego i łatwego w utrzymaniu kodu. Języki wspierające OOP to m.in. Java, C++, Python, C#, Smalltalk.

### Inne istniejące paradygmaty programowania

Paradygmat programowania to ogólny styl lub podejście do tworzenia programów, definiujące sposób organizacji kodu i wykonywania obliczeń. Większość nowoczesnych języków jest wieloparadygmatowa (np. Python, JavaScript), co pozwala łączyć różne podejścia.

Główne paradygmaty można podzielić na dwie szerokie kategorie: **imperatywne** (opisujące "jak" wykonać obliczenia krok po kroku) i **deklaratywne** (opisujące "co" ma być osiągnięte).

#### 1. Imperatywne

-   **Proceduralne (strukturalne)** Program to sekwencja procedur/funkcji i instrukcji zmieniających stan. Unika goto na rzecz struktur sterujących (pętle, warunki). Przykłady języków: C, Pascal, Go. Zalety: Proste, wydajne; wady: Trudne w dużych projektach (stan globalny).
-   **Obiektowe** Opisane powyżej – rozszerzenie proceduralnego o obiekty i klasy.

#### 2. Deklaratywne

-   **Funkcyjne** Traktuje obliczenia jako ewaluację funkcji matematycznych. Unika stanów zmiennych i efektów ubocznych (immutability). Funkcje są pierwszej klasy (można je przekazywać jako argumenty). Przykłady języków: Haskell (czysty), Lisp, Scala, F#. Zalety: Łatwe testowanie, równoległość; przydatne w przetwarzaniu danych.
-   **Logiczne** Program to zestaw faktów i reguł logicznych; silnik wnioskujący znajduje rozwiązanie. Przykłady języków: Prolog. Zalety: Idealne do AI, systemów ekspertowych; wady: Trudne w wydajnych obliczeniach.

#### Inne ważne paradygmaty

-   **Zdarzeniowe (event-driven)** Program reaguje na zdarzenia (np. kliknięcia myszy). Popularne w GUI i aplikacjach webowych. Przykłady: JavaScript (Node.js), aplikacje mobilne.
-   **Równoległe/współbieżne** Skupione na wykonywaniu wielu zadań jednocześnie (wątki, aktorzy). Przykłady: Erlang (model aktorów), Go (goroutines).
-   **Reaktywne** Program reaguje na strumienie danych i zmiany w czasie rzeczywistym. Przykłady: RxJS, Akka.
-   **Aspektowe (aspect-oriented)** Separuje cross-cutting concerns (np. logowanie, bezpieczeństwo) od głównej logiki.

Współczesne programowanie często łączy paradygmaty (np. OOP + funkcyjne w Pythonie czy Scali), co pozwala wybierać najlepsze narzędzie do danego problemu. Zrozumienie różnych paradygmatów pomaga pisać lepszy, bardziej elastyczny kod.

#### Brakująca cecha: Kompozycja (jako alternatywa dla dziedziczenia)

Kompozycja to mechanizm budowania złożonych obiektów poprzez włączenie (zawieranie) innych obiektów jako ich części składowe. Relacja "ma" zamiast "jest" (jak w dziedziczeniu). Jest preferowana w wielu przypadkach, ponieważ unika problemów z dziedziczeniem wielokrotnym i zwiększa elastyczność (zasada "favor composition over inheritance" z wzorców projektowych).

#### Zalety i wady OOP oraz porównanie z innymi paradygmatami

-   **Zalety**: Modularność, ponowne użycie kodu, łatwiejsze modelowanie złożonych systemów, lepsze utrzymanie.
-   **Wady**: Może być mniej wydajne (overhead obiektowy), nadużywanie dziedziczenia prowadzi do sztywnych hierarchii.
-   **Porównanie**: W przeciwieństwie do paradygmatu proceduralnego (sekwencja instrukcji), OOP skupia się na obiektach. Paradygmat funkcyjny unika stanów zmiennych, co kontrastuje z enkapsulacją OOP. W praktyce języki jak Python łączą OOP z innymi paradygmatami.


# Rodzaje Polimorfizmu

| Rodzaj polimorfizmu       | Kiedy decyzja o konkretnej metodzie? | Mechanizm w większości języków          | Przykład w praktyce                          | Najczęściej spotykany w       |
|---------------------------|---------------------------------------|------------------------------------------|-----------------------------------------------|-------------------------------|
| **Statyczny** (czas kompilacji) | W czasie kompilacji                  | Przeciążanie funkcji/metod/operatorów    | Różne sygnatury tej samej nazwy metody        | C++, Java, C#                 |
| **Dynamiczny** (czas wykonania) | W czasie wykonywania programu        | Nadpisywanie metod + późne wiązanie      | Wywołanie metody przez referencję do klasy bazowej | Prawie wszystkie języki OOP   |
| **Parametryczny** (generyczny)  | Częściowo kompilacja / częściowo runtime | Szablony / generyki                      | Lista<T>, ArrayList<T>                        | Java, C#, C++, TypeScript     |
| **Ad-hoc**                | Czas kompilacji                      | Przeciążanie operatorów, konwersje       | operator+, operator<< w C++                   | C++, Python (duck typing)     |


## Przykłady 

### Polimorfizm Statyczny (overload)
```
// Function to add two integers
void add(int a, int b) {
    cout << "Integer Sum = " << a + b
    << endl;
}

// Function to add two floating point values
void add(double a, double b) {
    cout << "Float Sum = " << a + b
    << endl ;
}
```

### Polimorfizm dynamiczny 

```
class Base {
public:

    // Virtual function
    virtual void display() {
        cout << "Base class function";
    }
};

class Derived : public Base {
public:

    // Overriding the base class function
    void display() override {
        cout << "Derived class function";
    }
};
```