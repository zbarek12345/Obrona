# Jakie protokoły stosuje się w rozległych sieci komputerowych. 
W sieciach rozległych (WAN - Wide Area Network), które łączą geograficznie oddalone lokalizacje (np. oddziały firmy w różnych miastach), wyzwania są inne niż w sieciach lokalnych (LAN). Tu priorytetem jest stabilność na długich dystansach, bezpieczeństwo danych przesyłanych przez infrastrukturę operatora oraz zarządzanie ruchem.

Protokoły te można podzielić na kilka kategorii w zależności od warstwy modelu OSI i zastosowania.

---

### 1. Protokoły Warstwy 2 (Łącza danych i Enkapsulacja)

Są to protokoły "opakowujące" dane, aby mogły przejść przez fizyczne łącza operatora telekomunikacyjnego.

* **PPP (Point-to-Point Protocol):**
* Uniwersalny standard dla połączeń bezpośrednich (punkt-punkt) między dwoma routerami.
* **Kluczowe cechy:** Obsługuje uwierzytelnianie (CHAP, PAP) – co jest kluczowe, by ISP wiedział, kto się łączy. Może łączyć wiele fizycznych łączy w jedno logiczne (Multilink PPP) dla zwiększenia przepustowości.
* *Wersja pochodna:* **PPPoE** (PPP over Ethernet) – powszechnie stosowana w usługach dostępu do Internetu (DSL, światłowód domowy).


* **HDLC (High-Level Data Link Control):**
* Starszy brat PPP. Jest domyślnym protokołem na łączach szeregowych w sprzęcie Cisco.
* Ma mniejszy narzut danych nagłówkowych niż PPP, ale jest mniej elastyczny (słaba obsługa uwierzytelniania i negocjacji).


* **Metro Ethernet / Carrier Ethernet:**
* **Współczesny standard.** Dawniej Ethernet był tylko w LAN. Dziś operatorzy (ISP) dostarczają łącza WAN, które zachowują się jak długi kabel Ethernet. Używa się tu standardów takich jak **802.1Q (VLAN tagging)** oraz **QinQ** (tunelowanie VLAN wewnątrz VLAN), aby separować ruch klientów w sieci operatora.



---

### 2. MPLS (Multiprotocol Label Switching) – "Warstwa 2.5"

To technologia, która zdominowała rynek korporacyjny przed erą SD-WAN. Nie jest typowym protokołem routingu ani warstwy 2, lecz czymś pośrodku.

* **Zasada działania:** Tradycyjny router dla każdego pakietu musi przeszukać całą tablicę routingu (co trwa). W MPLS routery na brzegu sieci nadają pakietom **krótkie etykiety (Labels)**.
* **Szybkość i kontrola:** Routery wewnątrz sieci operatora (rdzeń) nie patrzą na adresy IP, tylko błyskawicznie przełączają pakiety na podstawie etykiet.
* **Zastosowanie:** Umożliwia tworzenie **VPN w warstwie 3 (L3VPN)**, co pozwala łączyć oddziały firmy w jedną prywatną sieć, gwarantując przy tym parametry jakości (QoS) dla głosu i wideo.

---

### 3. Protokoły Routingu (Warstwa 3) – Skala globalna

W sieciach WAN, gdzie mamy tysiące tras, protokoły znane z LAN (jak OSPF) często nie wystarczają.

* **BGP (Border Gateway Protocol):**
* **Najważniejszy protokół Internetu.** Służy do wymiany informacji o trasach między **Systemami Autonomicznymi (AS)** – czyli między różnymi operatorami i dużymi firmami.
* **Cechy:** Jest wolniejszy w zbieżności niż OSPF, ale niesamowicie skalowalny (obsługuje pełną tablicę routingu Internetu – obecnie ponad 900 000 tras). Pozwala na skomplikowane sterowanie ruchem (polityki, atrybuty ścieżek).



---

### 4. Protokoły Tunelowania i VPN (Bezpieczeństwo przez Internet)

Gdy firma nie chce płacić za drogie łącza dedykowane (MPLS), korzysta ze zwykłego Internetu, tworząc bezpieczne tunele.

* **IPsec (Internet Protocol Security):**
* Zestaw protokołów zapewniających szyfrowanie, integralność i uwierzytelnianie pakietów IP.
* Używa **IKE (Internet Key Exchange)** do negocjacji kluczy. Jest fundamentem bezpiecznych połączeń Site-to-Site.


* **GRE (Generic Routing Encapsulation):**
* Prosty protokół tunelowania opracowany przez Cisco.
* **Wada:** Sam w sobie nie szyfruje danych.
* **Zaleta:** Potrafi przenosić pakiety multicast (czyli np. komunikaty routingu OSPF/EIGRP), czego czysty IPsec nie potrafi. Dlatego często stosuje się **GRE over IPsec** (GRE buduje tunel dla routingu, a IPsec go szyfruje).


* **DMVPN (Dynamic Multipoint VPN):**
* Rozwiązanie (głównie Cisco) pozwalające na tworzenie skalowalnych sieci VPN typu Hub-and-Spoke bez konieczności ręcznego konfigurowania tuneli między każdym oddziałem. Oddziały (Spokes) mogą dynamicznie tworzyć tunele między sobą.



---

### 5. Technologie schodzące (Legacy)

Warto je znać, bo wciąż można je spotkać w starych instalacjach lub w pytaniach egzaminacyjnych.

* **Frame Relay:** Popularny w latach 90. i 00. Przełączanie pakietów oparte na wirtualnych obwodach (DLCI). Wyparty przez MPLS i Metro Ethernet.
* **ATM (Asynchronous Transfer Mode):** Przesyłał dane w małych, stałych komórkach o wielkości 53 bajtów. Bardzo szybki i efektywny, ale skomplikowany i drogi. Był podstawą wczesnych sieci szkieletowych.

### Podsumowanie: Co wybrać dzisiaj?

Obecnie w nowoczesnych sieciach WAN króluje podejście hybrydowe lub **SD-WAN (Software-Defined WAN)**, które automatycznie dobiera protokół:

1. Dla danych krytycznych (VoIP, SAP) ruch idzie przez **MPLS**.
2. Dla danych mniej ważnych (YouTube, Facebook) ruch idzie przez tani Internet w tunelu **IPsec**.

Czy chciałbyś, abym wyjaśnił dokładniej, czym jest **SD-WAN** i dlaczego obecnie wypiera on tradycyjne routery w oddziałach firm?