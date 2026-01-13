# Szacowanie złożoności Algorytmów 
Szacowanie algorytmów to kluczowy element informatyki, który pozwala określić, jak wydajny będzie dany program wraz ze wzrostem ilości danych wejściowych ($n$). Najpowszechniejszą metodą opisu tej wydajności jest notacja dużego O ($O$).

Stopnie złożoności Algorytmów (Posortowane) (Nie oznacza to że algorytm złożoności głebiej położonej będzie wolniejszy od algorytmu złożoności lepszej ale o większym zbiorze. Prawie gwarantowane za to jest, że algorytm o wyższej złożoności będzie miał gorszy czas niż algorytm o lepszej złożoności dla tego samego problemu i zbioru. Prawie ponieważ zdarzają się wyjątki, gdy algorytm lepszej złożoności ma 'cold start' i algorytm mający hot start, ale gorszą złożoność jest go w stanie wyprzedzić.)

## 1. Złożoność stała: __$O(1)$__   
Algorytm wykonuje zawsze tyle samo operacji, niezależnie od tego, czy przetwarza 10 elementów, czy 10 milionów.
- Charakterystyka: Idealna wydajność.  
- Przykład: Pobranie elementu z tablicy pod konkretnym indeksem lub sprawdzenie, czy liczba jest parzysta.

## 2. Złożoność logarytmiczna: __$O(\log n)$__
Liczba operacji rośnie bardzo powoli w stosunku do wzrostu danych. Zazwyczaj występuje w algorytmach, które przy każdym kroku dzielą problem na pół.
- Charakterystyka: Bardzo wydajna dla ogromnych zbiorów danych.
- Przykład: Wyszukiwanie binarne w posortowanej tablicy. Aby znaleźć element w zbiorze miliarda rekordów, potrzeba zaledwie około 30 porównań.

## 3. Złożoność liniowa: __$O(n)$__ 
Czas wykonania rośnie proporcjonalnie do liczby elementów. Jeśli danych jest dwa razy więcej, czas pracy również wzrośnie dwukrotnie.
- Charakterystyka: Standardowa wydajność dla prostych operacji na listach.
- Przykład: Przeszukanie nieposortowanej listy w celu znalezienia konkretnej wartości lub zsumowanie wszystkich liczb w tablicy.

## 4. Złożoność liniowo-logarytmiczna: __$O(n \log n)$__
Najlepsza możliwa złożoność dla algorytmów sortowania opartych na porównaniach.
- Charakterystyka: Standard w nowoczesnych bibliotekach programistycznych.
- Przykład: Efektywne algorytmy sortowania, takie jak Merge Sort (sortowanie przez scalanie) lub Quick Sort.

## 5. Złożoność kwadratowa: __$O(n^2)$__
Liczba operacji rośnie z kwadratem liczby danych. Jeśli podwoimy ilość danych, algorytm będzie pracował cztery razy dłużej.
- Charakterystyka: Akceptowalna tylko dla małych zbiorów danych. Często wynika z zastosowania pętli w pętli.
- Przykład: Proste algorytmy sortowania, np. Sortowanie bąbelkowe (Bubble Sort) lub wstawianie elementu do każdej pary elementów w tablicy.

## 6. Złożoność wykładnicza: __$O(2^n)$__
Czas wykonania podwaja się przy dodaniu każdego kolejnego elementu. Bardzo szybko staje się nieużyteczna.
- Charakterystyka: Problemy uznawane za "trudne".
- Przykład: Rekurencyjne obliczanie ciągu Fibonacciego w naiwny sposób lub rozwiązywanie problemu wież Hanoi.

## 7. Złożoność silniowa: $O(n!)$

Najgorsza powszechnie spotykana złożoność. Nawet dla $n = 20$ liczba operacji jest astronomiczna.
- Charakterystyka: Rozwiązania typu "brute-force" (sprawdzanie wszystkich możliwości).
- Przykład: Problem komiwojażera – szukanie najkrótszej drogi między wszystkimi miastami poprzez sprawdzenie każdej możliwej kombinacji tras.

### __Porównanie Złożoności dla rozległości problemu__

| Notacja       | n=10  | n=100                 | n=1000                 |
|---------------|-------|-----------------------|------------------------|
| $O(1)$        | 1     | 1                     | 1                      |
| $O(\log n)$   | ~3    | ~7                    | ~10                    |
| $O(n)$        | 10    | 100                   | 1 000                  |
| $O(n \log n)$ | ~33   | ~664                  | ~10 000                |
| $O(n^2)$      | 100   | 10 000                | 1 000 000              |
| $O(2^n)$      | 1 024 | $1.26 \times 10^{30}$ | (brak miejsca na zera) |

Złożoność $N!$ nie została uwzględniona, z tej prostej przyczyny, że dla zbioru wielkości 10 elementów osiąga on już wartość 3628800.

# Znaki Granic przy złożoności algorytmu. 

## Notacja Wielkiego O ($O$) – "Górna granica"
To najczęściej używany symbol. Określa maksymalny czas wykonania algorytmu (pesymistyczny scenariusz). Mówi nam: "algorytm nie będzie działał wolniej niż to, ale może działać szybciej".

- Definicja: $f(n) = O(g(n))$ oznacza, że dla dużych danych funkcja $f$ rośnie co najwyżej tak szybko jak $g$.
- Intuicja: To jest nasz "limit prędkości". Jeśli algorytm ma $O(n^2)$, to mamy pewność, że w najgorszym przypadku nie przekroczy tej złożoności.

## 2. Notacja Wielkiej Omegi ($\Omega$) – "Dolna granica
"Określa minimalny czas wykonania algorytmu (optymistyczny scenariusz). Mówi nam: "algorytm nie będzie działał szybciej niż to, może być tylko tak samo lub gorzej".Definicja: $f(n) = \Omega(g(n))$ oznacza, że $g(n)$ jest dolnym ograniczeniem funkcji $f$.Przykład: Sortowanie przez wstawianie (Insertion Sort) ma złożoność $\Omega(n)$, gdy dane są już posortowane (najlepszy przypadek).Intuicja: To "gwarancja minimalnego wysiłku" – algorytm musi wykonać przynajmniej tyle pracy.

## 3. Notacja Wielkiej Tety ($\Theta$) – "Ciasna granica" 
To najbardziej precyzyjne oszacowanie. Stosujemy je, gdy górna i dolna granica są takie same. Mówi nam: "algorytm zachowuje się dokładnie tak, z dokładnością do stałej".
- Definicja: $f(n) = \Theta(g(n))$ wtedy i tylko wtedy, gdy $f(n) = O(g(n))$ oraz $f(n) = \Omega(g(n))$.
- Przykład: Przejście przez całą tablicę $n$-elementową zawsze zajmie $\Theta(n)$ – nie da się tego zrobić szybciej ani wolniej (jeśli musimy odwiedzić każdy element).Intuicja: "Złoty środek" – algorytm zachowuje się niemal identycznie w każdym przypadku.

## 4. Małe "o" oraz mała "omega" __($\omega$)__ 
Rzadziej używane w codziennym programowaniu, ale ważne w teorii:
- Małe $o$: Mówi, że jedna funkcja rośnie ściśle wolniej niż druga (nie mogą być równe). Na przykład $n = o(n^2)$. 
- Mała $\omega$: Mówi, że jedna funkcja rośnie ściśle szybciej niż druga.