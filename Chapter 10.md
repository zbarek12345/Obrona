# Fizyczne nośniki danych – stosowane technologie, struktury oraz metody kodowania informacji.
To temat rzeka, który łączy w sobie fizykę ciała stałego, inżynierię materiałową oraz teorię informacji. Aby zachować czytelność, podzielimy to zagadnienie na trzy główne filary technologiczne: **magnetyczne, optyczne i półprzewodnikowe**, a na końcu omówimy warstwę logiczną (systemy plików) zależną od systemu operacyjnego.

Oto szczegółowy opis technologii, struktur i metod kodowania.

---

### 1. Nośniki Magnetyczne (HDD, Taśmy, Dyskietki)

Najstarsza i przez lata dominująca technologia masowa.

#### Technologia i Fizyka

Dane są zapisywane poprzez zmianę polaryzacji domen magnetycznych na powierzchni talerza (lub taśmy).

* **Głowice:** Ewoluowały od indukcyjnych do **GMR** (Gigantyczny Magnetoopór) i **TMR** (Tunelowy Magnetoopór), co pozwoliło na drastyczne zwiększenie gęstości zapisu.
* **Zapis prostopadły (PMR) vs SMR/HAMR:** W starszych dyskach domeny leżały płasko. Nowoczesne dyski (od ok. 2005 r.) stosują zapis prostopadły (PMR), co pozwala upakować więcej danych. Najnowsze technologie to HAMR (zapis wspomagany ciepłem lasera).

#### Struktura Fizyczna

* **Talerze (Platters):** Wirujące dyski pokryte warstwą ferromagnetyczną.
* **Ścieżki (Tracks) i Cylindry:** Koncentryczne okręgi na talerzu. Zbiór tych samych ścieżek na wszystkich talerzach tworzy cylinder.
* **Sektory:** Najmniejsza fizyczna jednostka zapisu. Przez dekady wynosiła **512 bajtów**, obecnie standardem jest „Advanced Format” (**4096 bajtów** / 4K), co zwiększa efektywność korekcji błędów ECC.

#### Metody Kodowania Sygnału (Fizyczne)

Surowe bity nie mogą być zapisane bezpośrednio (ciąg samych zer mógłby zgubić synchronizację głowicy).

1. **FM (Frequency Modulation):** Historyczna, stosowana w starych dyskietkach (Single Density).
2. **MFM (Modified Frequency Modulation):** Kodowanie stosowane w dyskietkach HD i wczesnych dyskach twardych. Zmniejsza liczbę koniecznych zmian strumienia magnetycznego.
3. **RLL (Run Length Limited):** Przełom w latach 80/90. Pozwala na gęstszy zapis poprzez mapowanie grup bitów na wzorce magnetyczne, zapewniając, że odstępy między zmianami strumienia nie są ani za małe, ani za duże.
4. **PRML (Partial Response Maximum Likelihood):** Współczesny standard. Zamiast czytać "0" lub "1", elektronika dysku próbkuje sygnał analogowy i używa zaawansowanych algorytmów (podobnych do Viterbiego), by "odgadnąć" najbardziej prawdopodobną sekwencję bitów.

---

### 2. Nośniki Optyczne (CD, DVD, Blu-ray)

Technologia oparta na świetle lasera i odbiciach.

#### Technologia

* **CD (1982):** Laser podczerwony (780 nm).
* **DVD (1995):** Laser czerwony (650 nm) – krótsza fala pozwoliła na gęstsze upakowanie.
* **Blu-ray (2006):** Laser niebiesko-fioletowy (405 nm).

#### Struktura Fizyczna

W przeciwieństwie do HDD, nośniki optyczne mają zazwyczaj **jedną spiralną ścieżkę** biegnącą od środka do krawędzi (jak płyta winylowa).

* **Pits (wgłębienia) i Lands (pola):** Laser odbija się od pola, a rozprasza na wgłębieniu (lub zmienia się faza światła). Co ciekawe, logiczna "1" to nie "wgłębienie", ale **moment przejścia** między wgłębieniem a polem. Brak zmiany to "0".

#### Metody Kodowania (Modulacja)

* **EFM (Eight-to-Fourteen Modulation):** Stosowane w CD. Każde 8 bitów danych zamieniane jest na 14 bitów kodu (plus bity łączące). Zapobiega to występowaniu zbyt bliskich przejść (fizycznie niemożliwych do odczytu przez laser).
* **EFMPlus:** Ulepszona wersja dla DVD (8 bitów na 16 bitów kodu), bardziej efektywna.
* **Korekcja błędów (Reed-Solomon):** Kluczowa w optyce. Płyta CD może być porysowana, a dane są odzyskiwane dzięki przeplataniu (CIRC – Cross-Interleaved Reed-Solomon Coding).

---

### 3. Pamięci Półprzewodnikowe (Flash NAND – SSD, SD, USB)

Obecny standard wydajności. Brak części mechanicznych.

#### Technologia: Tranzystor z bramką pływającą

Podstawą jest tranzystor MOSFET, który posiada dodatkową "bramkę pływającą" (Floating Gate) izolowaną tlenkiem. Elektrony są tam "wpychane" pod wysokim napięciem (efekt tunelowy) i zostają uwięzione, zmieniając napięcie progowe tranzystora.

#### Ewolucja gęstości zapisu (Struktura komórki)

To kluczowe dla rozróżnienia wydajności i trwałości:

1. **SLC (Single Level Cell):** 1 bit na komórkę (tylko stany 0 i 1). Najszybsze, najtrwalsze, najdroższe. (Przemysł).
2. **MLC (Multi Level Cell):** 2 bity na komórkę (4 poziomy napięcia).
3. **TLC (Triple Level Cell):** 3 bity na komórkę (8 poziomów napięcia). Standard dzisiaj.
4. **QLC (Quad Level Cell):** 4 bity (16 poziomów napięcia!). Tanie, ale wolniejsze i mniej trwałe.

#### Struktura logiczno-fizyczna

Pamięć Flash ma specyficzną budowę, która wymusza stosowanie skomplikowanych kontrolerów:

* **Page (Strona):** Jednostka odczytu i zapisu (np. 4 KB lub 16 KB).
* **Block (Blok):** Jednostka kasowania. **Nie można nadpisać strony, trzeba skasować cały blok (np. 128 stron).** To wymusza procesy takie jak *Garbage Collection* i *Wear Leveling* (równoważenie zużycia).

---

### 4. Systemy plików i struktury logiczne (Zależność od OS i Czasu)

Fizyczny nośnik to tylko "magazyn". Aby system operacyjny widział pliki, potrzebny jest system plików.

| Epoka / System | System Plików | Cechy charakterystyczne i struktura |
| --- | --- | --- |
| **DOS / Win 9x** | **FAT (12/16/32)** | **Tablica Alokacji Plików.** Prosta lista klastrów. Brak zabezpieczeń, duża fragmentacja. Uniwersalny (czytany przez wszystko). |
| **Windows NT/XP/10/11** | **NTFS** | Oparty na **MFT (Master File Table)**. Obsługuje uprawnienia (ACL), księgowanie (journaling - odporność na awarie zasilania), kompresję. |
| **Linux (Wczesny)** | **ext2** | Oparty na i-węzłach (inodes). Szybki, ale brak księgowania (ryzyko utraty danych przy awarii). |
| **Linux (Współczesny)** | **ext4, XFS, Btrfs** | **ext4:** Standard z księgowaniem. **Btrfs/ZFS:** Systemy nowej generacji (COW - Copy on Write), obsługują migawki (snapshots) i sumy kontrolne danych (ochrona przed *bit rot*). |
| **macOS (do 2017)** | **HFS+** | Przestarzały system z lat 90. Problemy z wielowątkowością. |
| **macOS (od 2017)** | **APFS** | **Apple File System.** Zoptymalizowany pod **SSD**. Błyskawiczne klonowanie plików, szyfrowanie natywne, dynamiczna alokacja przestrzeni między partycjami. |

### Podsumowanie różnic w kodowaniu

* **Magnetyczne:** Walczą z szumem i synchronizacją (RLL, PRML).
* **Optyczne:** Walczą z fizyką lasera i uszkodzeniami powierzchni (EFM, Reed-Solomon).
* **Flash:** Walczą z zużyciem komórek i precyzją napięć (Wear Leveling, kody ECC BCH/LDPC).

Czy chciałbyś, abym dokładniej wyjaśnił różnicę między interfejsem **SATA (AHCI)** a **NVMe** w kontekście nowoczesnych dysków SSD, ponieważ to one determinują, jak szybko procesor "rozmawia" z nośnikiem?