Metoda śledzenia promieni (Ray Tracing) to zaawansowana technika renderowania grafiki 3D, która naśladuje fizyczne zachowanie światła w świecie rzeczywistym. W przeciwieństwie do tradycyjnej rasteryzacji, ray tracing "śledzi" drogę promieni świetlnych, co pozwala na uzyskanie fotorealistycznych efektów.

## 1. Koncepcja Odwróconego Śledzenia
W rzeczywistości miliardy promieni słonecznych odbijają się od przedmiotów i tylko ułamek trafia do naszego oka. Renderowanie takiej ilości danych byłoby niemożliwe. Ray tracing stosuje więc sprytną sztuczkę: śledzi promienie wstecz.

__Promień Pierwotny (Primary Ray)__: Wypuszczany jest z "oka" (kamery) przez każdy piksel płaszczyzny obrazu w głąb sceny 3D.

__Punkt Przecięcia__: Algorytm sprawdza, w który najbliższy obiekt uderzył promień.

__Obliczanie Koloru__: W miejscu uderzenia algorytm sprawdza właściwości materiału (kolor, tekstura) oraz oświetlenie.

## 2. Kluczowe Efekty Fizyczne
To, co czyni ray tracing wyjątkowym, to sposób obsługi zjawisk optycznych poprzez generowanie promieni wtórnych:

__Cienie (Shadow Rays)__: Od punktu uderzenia wysyłany jest promień w stronę każdego źródła światła. Jeśli po drodze napotka przeszkodę – punkt jest w cieniu. Pozwala to na uzyskanie miękkich, realistycznych cieni.

__Odbicia (Reflections)__: Jeśli obiekt jest lustrzany, wysyłany jest nowy promień pod kątem odbicia. Algorytm sprawdza, co widzi ten promień, i nanosi to na obiekt.

__Załamania (Refraction)__: Gdy promień uderza w przezroczysty obiekt (szkło, woda), zmienia on kierunek zgodnie ze współczynnikiem załamania światła materiału.

__Okluzja otoczenia (Ambient Occlusion)__: Pozwala na uzyskanie realistycznych przyciemnień w rogach i zagłębieniach, gdzie światło dociera trudniej.

## 3. Algorytm Krok po Kroku
Proces generowania obrazu można podzielić na etapy obliczeniowe:

__Emisja__: Dla każdego piksela ekranu wyślij promień.

__Test Przecięcia (Intersection Test)__: Matematyczne obliczenie punktu styku promienia z geometrią (np. sferą, trójkątem).

__Cieniowanie (Shading)__: Zastosowanie modelu oświetlenia (np. Phonga lub PBR – Physically Based Rendering).

__Rekurencja__: Jeśli powierzchnia jest odbijająca lub przezroczysta, powtórz proces dla nowych promieni (aż do osiągnięcia limitu odbić, tzw. Ray Depth).

__Rekonstrukcja__: Zebranie wyników ze wszystkich promieni i uśrednienie ich (Anti-aliasing) w celu uzyskania finalnego piksela.

## 4. Wyzwania i Nowoczesne Rozwiązania
Ray tracing jest niezwykle kosztowny obliczeniowo. Aby go przyspieszyć, stosuje się:

- BVH (Bounding Volume Hierarchy): Drzewiasta struktura danych, która pozwala szybko odrzucić obiekty, w które promień na pewno nie uderzy, zamiast sprawdzać każdy trójkąt w scenie.

- Denoising (Odnośnianie): Algorytmy AI (np. NVIDIA DLSS), które usuwają szum z obrazu wygenerowanego przy użyciu małej liczby promieni.

- Śledzenie Ścieżek (Path Tracing): Bardziej zaawansowana odmiana, która losuje kierunki odbić, co pozwala na uzyskanie Global Illumination (światło odbite od jednej ściany oświetla drugą, przenosząc jej kolor).

| Cecha     | Rasteryzacja                  | Ray Tracing                         |
|-----------|-------------------------------|-------------------------------------|
| Szybkość  | Bardzo wysoka (Gry)           | Niska (Filmy / Nowoczesne GPU)      |
| Cienie    | Mapy cieni (często z błędami) | Fizycznie poprawne                  |
| Odbicia   | Przybliżone (Screen Space)    | Realistyczne (nawet poza ekranem)   |
| Złożoność | $O(N)$ (liczba wielokątów)    | $O(\log N)$ (dzięki strukturom BVH) |