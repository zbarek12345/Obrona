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