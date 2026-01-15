# Projektowanie sieci
Projektowanie sieci komputerowych to złożony proces inżynieryjny, którego celem jest stworzenie infrastruktury, która jest nie tylko „działająca”, ale także wydajna, bezpieczna, skalowalna i łatwa w zarządzaniu. W inżynierii sieciowej (np. w standardach Cisco czy Juniper) wyróżnia się ścisłe metodologie i modele architektoniczne.

Oto dokładny opis zasad projektowania sieci, podzielony na warstwy logiczne, fizyczne i metodologiczne.

---

### 1. Model Hierarchiczny (Trójwarstwowy)

To absolutny fundament projektowania nowoczesnych sieci kampusowych i korporacyjnych (LAN). Zamiast płaskiej struktury (gdzie wszystko jest połączone ze wszystkim), stosuje się podział na moduły o ściśle określonych funkcjach.

* **Warstwa Dostępu (Access Layer):**
* **Funkcja:** Punkt styku użytkowników końcowych (PC, drukarki, punkty Wi-Fi) z siecią.
* **Zadania:** Tutaj realizuje się polityki bezpieczeństwa na poziomie portu (Port Security, 802.1X), zasilanie urządzeń (PoE - Power over Ethernet) oraz segmentację VLAN.
* **Sprzęt:** Switche L2 (Layer 2), charakteryzujące się dużą gęstością portów i niższym kosztem.


* **Warstwa Dystrybucji (Distribution Layer):**
* **Funkcja:** Agreguje połączenia z warstwy dostępu i łączy je z rdzeniem. Jest granicą między domenami L2 (przełączanie) i L3 (rutowanie).
* **Zadania:** Routing między sieciami VLAN (Inter-VLAN routing), filtrowanie pakietów (ACL), sumaryzacja tras (route summarization) oraz redystrybucja protokołów routingu.
* **Sprzęt:** Wydajne switche wielowarstwowe (L3) lub routery.


* **Warstwa Rdzenia (Core Layer):**
* **Funkcja:** Szybki szkielet sieci (Backbone). Ma za zadanie jak najszybciej przesłać pakiety między blokami dystrybucyjnymi.
* **Zadania:** Tutaj **nie wykonuje się** skomplikowanych operacji obciążających procesor (jak filtrowanie ACL czy inspekcja pakietów). Liczy się tylko szybkość i niezawodność.
* **Sprzęt:** Bardzo wydajne switche/routery z łączami światłowodowymi (10G/40G/100G).



---

### 2. Kluczowe Zasady Architektoniczne

#### A. Redundancja i Wysoka Dostępność (High Availability)

Sieć musi być odporna na awarie (Single Point of Failure – SPOF).

* **Redundancja fizyczna:** Dublowanie kluczowych urządzeń (dwa routery brzegowe, dwa switche rdzeniowe) oraz dublowanie łączy (każdy switch dostępowy podłączony do dwóch switchy dystrybucyjnych).
* **Protokoły logiczne:** Aby pętle fizyczne nie „zabiły” sieci, stosuje się mechanizmy logiczne:
* **STP (Spanning Tree Protocol):** Blokuje nadmiarowe ścieżki w warstwie L2, odblokowując je w razie awarii.
* **FHRP (First Hop Redundancy Protocol):** Np. HSRP lub VRRP. Pozwala dwóm routerom udawać jeden wirtualny adres bramy (Gateway). Jeśli główny padnie, zapasowy przejmuje ruch natychmiast.
* **EtherChannel / LACP:** Łączenie kilku fizycznych kabli w jeden logiczny kanał. Daje to większą przepustowość i odporność na zerwanie pojedynczego kabla.



#### B. Skalowalność (Scalability)

Projekt musi uwzględniać wzrost sieci w przyszłości bez konieczności jej przebudowywania (tzw. "fork-lift upgrade").

* **Modułowość:** Sieć buduje się z bloków (np. blok kampusu, blok Data Center, blok styku z Internetem). Gdy firma rośnie, dodajemy nowy blok dystrybucyjny, nie ruszając rdzenia.
* **Adresacja IP:** Hierarchiczny plan adresacji IP jest kluczowy. Pozwala na **sumaryzację tras** (route summarization). Dzięki temu routery w rdzeniu przechowują np. 1 wpis dla całej podsieci oddziału, zamiast 500 wpisów dla poszczególnych podsieci VLAN.

#### C. Średnica Sieci (Network Diameter)

Jest to liczba urządzeń (przeskoków/hops), przez które musi przejść pakiet, aby dotrzeć od nadawcy do odbiorcy.

* **Zasada:** Projektujemy sieć tak, aby średnica była niska i przewidywalna. Model hierarchiczny gwarantuje deterministyczny czas przesyłu. Niekontrolowane łączenie switchy w szereg (tzw. *daisy-chaining*) jest błędem projektowym, zwiększającym opóźnienia i ryzyko awarii.

---

### 3. Projektowanie Logiczne (Layer 2 i Layer 3)

#### Segmentacja (VLAN)

Nigdy nie budujemy dużych, płaskich sieci. Dzielimy sieć na wirtualne sieci lokalne (VLAN).

* **Ograniczenie domen rozgłoszeniowych (Broadcast Domains):** Ruch typu broadcast (np. zapytania ARP) nie powinien zalewać całej sieci, a jedynie mały wycinek (np. dział księgowości).
* **Bezpieczeństwo:** Użytkownik z VLANu "Goście" nie ma fizycznego dostępu do pakietów z VLANu "Serwery", chyba że ruch przejdzie przez router/firewall z odpowiednimi regułami.

#### Dobór Protokołów Routingu

W zależności od wielkości sieci wybiera się protokół dynamicznego routingu:

* **OSPF (Open Shortest Path First):** Standard w sieciach korporacyjnych. Szybko reaguje na zmiany (zbieżność/convergence), uwzględnia przepustowość łącza.
* **EIGRP:** Własnościowy protokół Cisco (obecnie częściowo otwarty), bardzo prosty w konfiguracji i wydajny.
* **BGP (Border Gateway Protocol):** Stosowany na styku z Internetem (ISP) lub w bardzo dużych sieciach Data Center.

---

### 4. Metodologia Projektowania: Cykl Życia Sieci (PPDIOO)

Profesjonalne podejście (np. wg Cisco) nie kończy się na wdrożeniu.

1. **Prepare (Przygotowanie):** Analiza wymagań biznesowych, budżetu i celów.
2. **Plan (Planowanie):** Audyt obecnej infrastruktury, analiza luk.
3. **Design (Projektowanie):** Właściwy etap tworzenia schematów topologii, planu adresacji IP, wyboru sprzętu.
4. **Implement (Wdrożenie):** Instalacja, konfiguracja sprzętu.
5. **Operate (Eksploatacja):** Codzienne utrzymanie, monitoring (SNMP, Syslog).
6. **Optimize (Optymalizacja):** Analiza błędów, poprawa wydajności, przygotowanie do ponownego cyklu.

### 5. Obliczenia i Wymiarowanie (Capacity Planning)

Projektant musi przeprowadzić obliczenia zapotrzebowania na pasmo (Bandwidth). Należy uwzględnić:

* **Oversubscription (Nadsubskrypcja):** W warstwie dostępu rzadko kiedy wszyscy użytkownicy wysyłają dane z pełną prędkością naraz. Typowy bezpieczny stosunek przepustowości portów dostępowych do wyjściowych (uplink) to **20:1** dla zwykłych danych.
* **QoS (Quality of Service):** Jeśli w sieci będzie działać telefonia VoIP lub wideokonferencje, projekt musi gwarantować priorytetyzację tego ruchu i minimalne opóźnienia (Jitter).

### Podsumowanie: Najczęstsze błędy

1. Brak redundancji w warstwie rdzenia (awaria wyłącza całą firmę).
2. Zbyt duża domena rozgłoszeniowa (np. 1000 komputerów w jednej podsieci IP).
3. Brak dokumentacji i etykietowania kabli (koszmar przy awarii).

Ponieważ poruszyłem temat adresacji: **Czy chciałbyś, abym przedstawił proces projektowania adresacji IP (subnettingu) na konkretnym przykładzie, np. dla firmy posiadającej 3 działy?**
