# Synchronizacja Procesów

Synchronizacja procesów to jedno z najtrudniejszych zadań systemu operacyjnego. Jej celem jest zapewnienie, że współbieżne procesy (lub wątki) nie będą jednocześnie modyfikować tych samych danych, co mogłoby prowadzić do wyścigu (race condition).

Systemy operacyjne dostarczają zestaw mechanizmów, które pozwalają zarządzać dostępem do tzw. sekcji krytycznej.

## 1. Semafory (Semaphores)
Wprowadzone przez Edsgera Dijkstrę, są jednym z najstarszych i najpopularniejszych mechanizmów. Semafory to zmienne liczbowe sterowane dwiema atomowymi operacjami: wait() (P) oraz signal() (V).

- Semafory binarne (Muteksy): Przyjmują wartości 0 lub 1. Działają jak rygiel w drzwiach – albo proces ma dostęp, albo nie.

- Semafory licznikowe: Przyjmują wartości całkowite nieujemne. Reprezentują liczbę dostępnych zasobów (np. 5 wolnych miejsc w buforze).

## 2. Muteksy (Mutex – Mutual Exclusion)
Muteks to uproszczona wersja semafora binarnego, która posiada unikalną cechę: własność (ownership). Tylko proces, który zablokował muteks, może go odblokować.

Zastosowanie: Ścisła ochrona pojedynczego obiektu lub fragmentu kodu przed jednoczesnym dostępem.

Zaleta: Zapobiega sytuacjom, w których jeden proces przypadkowo zwalnia blokadę nałożoną przez inny.

## 3. Monitory
Monitory to mechanizm wyższego poziomu (często zaimplementowany w językach programowania jak Java przy wsparciu OS). Monitor to "bezpieczny obiekt", w którym w danej chwili może znajdować się tylko jeden proces.

Zmienne warunkowe: Pozwalają procesom "zasnąć" wewnątrz monitora (wait), czekając na spełnienie specyficznego warunku, oraz budzić inne procesy (signal), gdy warunek zostanie spełniony.

Zaleta: Automatyzują blokowanie i odblokowywanie, co zmniejsza ryzyko błędów programistycznych.

## 4. Zmienne Warunkowe (Condition Variables)
Służą do powiadamiania między procesami o zmianie stanu zasobu. Zawsze działają w parze z muteksem.

- Proces sprawdza warunek. Jeśli nie jest spełniony, wywołuje wait na zmiennej warunkowej, co jednocześnie zwalnia muteks i usypia proces.

- Inny proces, po zmianie stanu, wywołuje signal (budzi jeden proces) lub broadcast (budzi wszystkie), aby ponownie sprawdziły warunek.

## 5. Bariery (Barriers)
Mechanizm stosowany w obliczeniach równoległych. Żaden proces nie może przejść przez "barierę", dopóki wszystkie biorące udział procesy do niej nie dotrą.

- Przykład: Renderowanie klatki filmu – procesor musi poczekać, aż wszystkie wątki skończą obliczać swoje części obrazu, zanim przejdzie do następnej klatki.

## Typowe Problemy i Zagrożenia
Podczas stosowania powyższych mechanizmów system operacyjny musi radzić sobie z dwoma zjawiskami:

| Problem                  | Opis                                                                                                                  |
|--------------------------|-----------------------------------------------------------------------------------------------------------------------|
| Zakleszczenie (Deadlock) | Dwa procesy czekają na siebie nawzajem (A trzyma zasób 1 i chce zasób 2; B trzyma 2 i chce 1). Żaden nie może ruszyć. |
| Głodzenie (Starvation)   | Proces o niskim priorytecie nigdy nie dostaje dostępu do sekcji krytycznej, bo zawsze wyprzedzają go inne procesy.    |
| Inwersja priorytetów     | Proces o niskim priorytecie blokuje zasób potrzebny procesowi o wysokim priorytecie, co paraliżuje system.            |

# Muteks a Semafor
To doskonałe pytanie, które dotyka sedna różnicy między prostymi narzędziami a wyspecjalizowanymi mechanizmami. __Krótka odpowiedź brzmi__: koncepcyjnie muteks jest bardzo podobny do semfora binarnego, ale w praktyce systemów operacyjnych są to dwa różne byty. Oto dokładne wyjaśnienie ich relacji:  
## 1. Perspektywa teoretyczna: Muteks jako semafor  
W sensie czysto matematycznym i algorytmicznym, muteks można traktować jako semafor binarny, czyli taki, który może przyjmować tylko dwie wartości: $0$ (zablokowany) lub $1$ (wolny). Oba mechanizmy służą do realizacji wzajemnego wykluczenia (Mutual Exclusion).  
## 2. Kluczowe różnice (Dlaczego to nie to samo?)  
Choć działają podobnie, istnieją fundamentalne różnice w ich przeznaczeniu i zachowaniu:  
__A. Własność (Ownership)__ 
- Najważniejsza różnicaMuteks: Ma właściciela. Tylko ten wątek, który "zamknął" muteks, ma prawo go "otworzyć". To mechanizm ochrony zasobu.  
- Semafor: Nie ma właściciela. Jeden wątek może wywołać wait() (zająć zasób), a zupełnie inny może wywołać signal() (zwolnić go). To mechanizm sygnalizacji.   

__B. Przeznaczenie__  
- Muteks: Służy wyłącznie do wzajemnego wykluczania (dostęp do sekcji krytycznej).Semafor: Służy do synchronizacji (np. "poinformuj mnie, gdy dane będą gotowe") lub zarządzania pulą wielu zasobów (semafor licznikowy).  
C. Bezpieczeństwo i Inwersja PriorytetówWspółczesne systemy operacyjne implementują w muteksach mechanizmy, których semafory zazwyczaj nie posiadają:
- Dziedziczenie priorytetów: Jeśli proces o niskim priorytecie trzyma muteks, którego potrzebuje proces o wysokim priorytecie, OS tymczasowo podnosi priorytet tego pierwszego, aby jak najszybciej zwolnił blokadę. W semaforach (z racji braku właściciela) jest to niemożliwe.