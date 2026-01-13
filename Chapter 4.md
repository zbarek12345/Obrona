# Model warstwowy TCP / IP 

![img](https://pasja-informatyki.pl/pliki/model-tcp-ip.jpg)

Jak widać model ten składa się z 4 warstw odpowiadających za następujące części opisane poniżej. 

|Warstwa|
|:-----:|
|[Aplikacji](#1-warstwa-aplikacji)|
|[Transportu](#2-warstwa-transportu)|
|[Internetowa](#3-warstwa-internetowa)|
|[Dostępu do Sieci](#4-warstwa-dostępu-do-sieci)|

## 1. Warstwa Aplikacji.
### Warstwa aplikacji w modelu TCP/IP
Model TCP/IP, znany również jako model DoD (Department of Defense), jest uproszczoną wersją modelu OSI i składa się z czterech warstw: warstwy dostępu do sieci (Network Access Layer), warstwy internetowej (Internet Layer), warstwy transportowej (Transport Layer) oraz warstwy aplikacji (Application Layer). Warstwa aplikacji jest najwyższą warstwą w tym modelu i pełni kluczową rolę w komunikacji między aplikacjami użytkownika a siecią. W przeciwieństwie do modelu OSI, gdzie funkcje te są rozdzielone na trzy warstwy (aplikacji, prezentacji i sesji), w TCP/IP są one zintegrowane w jedną warstwę aplikacji. Poniżej opiszę ją szczegółowo, w tym jej funkcje, cechy oraz popularne protokoły stosowane w tej warstwie.  
### Funkcje i cechy warstwy aplikacji
Warstwa aplikacji jest odpowiedzialna za interakcję między oprogramowaniem użytkownika (np. przeglądarkami internetowymi, klientami pocztowymi czy aplikacjami do transferu plików) a niższymi warstwami modelu TCP/IP. Nie zajmuje się ona samym transportem danych przez sieć (to zadanie warstwy transportowej i niższych), ale zapewnia interfejsy i mechanizmy umożliwiające aplikacjom wysyłanie i odbieranie danych w sposób zrozumiały dla użytkownika.
__Kluczowe funkcje warstwy aplikacji__:

- Udostępnianie usług sieciowych: Warstwa ta definiuje protokoły, które umożliwiają aplikacjom dostęp do zasobów sieciowych, takich jak strony internetowe, pliki, e-maile czy bazy danych. Protokoły te działają na poziomie aplikacji końcowej, co oznacza, że są niezależne od sprzętu sieciowego.
- Zarządzanie sesjami: Chociaż w TCP/IP nie ma oddzielnej warstwy sesji, funkcje te są wbudowane w protokoły aplikacyjne. Obejmuje to nawiązywanie, utrzymywanie i kończenie połączeń między aplikacjami (np. logowanie do serwera).
- Konwersja i formatowanie danych: Warstwa aplikacji obsługuje prezentację danych, w tym kodowanie (np. ASCII, UTF-8), kompresję i szyfrowanie. Na przykład, konwertuje dane z formatu używanego przez aplikację (np. HTML) na format nadający się do transmisji.
- Bezpieczeństwo i uwierzytelnianie: Wiele protokołów w tej warstwie włącza mechanizmy uwierzytelniania (np. hasła, certyfikaty), autoryzacji i szyfrowania, aby chronić dane przed nieautoryzowanym dostępem.
- Interakcja z użytkownikiem: Warstwa ta jest najbliższa użytkownikowi, umożliwiając bezpośrednią interakcję poprzez interfejsy graficzne lub wiersz poleceń. Na przykład, przeglądarka internetowa używa protokołu HTTP do pobierania stron WWW.
- Abstrakcja od niższych warstw: Aplikacje nie muszą wiedzieć, jak dane są routowane przez sieć (to rola warstwy internetowej) czy jak zapewniana jest niezawodność transmisji (warstwa transportowa). Warstwa aplikacji po prostu "rozmawia" z aplikacjami po drugiej stronie połączenia.

__Cechy charakterystyczne__:
- Protokoły oparte na porcie: Protokoły aplikacyjne używają numerów portów (z zakresu 0-65535) do identyfikacji usług. Na przykład, port 80 dla HTTP. Numery portów są zarządzane przez IANA (Internet Assigned Numbers Authority).
- Klient-serwer lub peer-to-peer: Większość protokołów działa w modelu klient-serwer (np. klient żąda zasobów od serwera), ale niektóre wspierają P2P (np. BitTorrent).
Niezależność od systemu operacyjnego: Protokoły są standardowe i działają na różnych platformach (Windows, Linux, macOS).
- Ewolucja: Warstwa aplikacji jest dynamiczna – nowe protokoły powstają w odpowiedzi na potrzeby, np. HTTPS dla bezpieczeństwa czy WebSocket dla komunikacji w czasie rzeczywistym.
- Zależność od warstwy transportowej: Protokoły aplikacyjne zazwyczaj korzystają z TCP (dla niezawodnej transmisji) lub UDP (dla szybkiej, ale mniej niezawodnej).

Warstwa aplikacji nie jest ściśle zdefiniowana w RFC (Request for Comments) modelu TCP/IP, co pozwala na elastyczność, ale może prowadzić do niejednoznaczności w porównaniu z modelem OSI.

__Popularne protokoły stosowane w warstwie aplikacji__  
Poniżej przedstawiam tabelę z wybranymi popularnymi protokołami warstwy aplikacji w modelu TCP/IP. Wybrałem te najbardziej powszechne, z krótkim opisem ich funkcji, cech, portów domyślnych oraz przykładów użycia. Tabela jest uporządkowana alfabetycznie dla ułatwienia.

|                 Protokół                |                                                                                                                                                                          Opis szczegółowy                                                                                                                                                                          |            Domyślny port            |            Protokół transportowy           |                                       Przykłady użycia                                      |
|:---------------------------------------:|:------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------:|:-----------------------------------:|:------------------------------------------:|:-------------------------------------------------------------------------------------------:|
| DNS (Domain Name System)                | Protokół tłumaczący nazwy domen (np. example.com) na adresy IP. Działa w modelu klient-serwer, obsługuje zapytania rekurencyjne i iteracyjne. Wspiera typy rekordów jak A (IPv4), AAAA (IPv6), MX (poczta), CNAME (aliasy). Jest kluczowy dla funkcjonowania internetu, zapobiegając potrzebie zapamiętywania adresów IP. Może używać cache'owania dla wydajności. | 53                                  | UDP (głównie), TCP (dla dużych odpowiedzi) | Przeglądanie stron WWW, wysyłanie e-maili; serwery jak Google DNS (8.8.8.8).                |
| FTP (File Transfer Protocol)            | Protokół do transferu plików między klientem a serwerem. Obsługuje tryby aktywne i pasywne, uwierzytelnianie (login/hasło), komendy jak GET, PUT, LIST. Jest starszy i mniej bezpieczny (dane w plaintext), dlatego często zastępowany przez SFTP lub FTPS. Wspiera wznowienie transferu po przerwaniu.                                                            | 21 (kontrola), 20 (dane)            | TCP                                        | Przesyłanie plików na serwery hostingowe, pobieranie oprogramowania; klienty jak FileZilla. |
| HTTP (HyperText Transfer Protocol)      | Protokół do transferu hipertekstu (stron WWW). Obsługuje metody jak GET, POST, PUT, DELETE. Jest bezstanowy (każde żądanie niezależne), ale może używać ciasteczek dla sesji. Wersja HTTP/1.1 wprowadziła persistent connections, HTTP/2 – multipleksowanie, HTTP/3 – QUIC dla szybszej transmisji.                                                                | 80                                  | TCP (HTTP/1.x i 2), UDP (HTTP/3 via QUIC)  | Przeglądanie stron internetowych; serwery jak Apache, Nginx.                                |
| HTTPS (HTTP Secure)                     | Wersja HTTP z szyfrowaniem SSL/TLS. Zapewnia poufność, integralność i uwierzytelnianie poprzez certyfikaty (np. Let's Encrypt). Obsługuje handshake TLS dla negocjacji kluczy. Jest standardem dla bezpiecznych transakcji, redukując ryzyko ataków man-in-the-middle.                                                                                             | 443                                 | TCP (z TLS)                                | Zakupy online, logowanie do kont; prawie wszystkie nowoczesne strony WWW.                   |
| IMAP (Internet Message Access Protocol) | Protokół do dostępu do poczty e-mail na serwerze. Pozwala na zarządzanie folderami, wyszukiwanie, flagowanie wiadomości bez pobierania ich wszystkich. Wspiera IDLE dla powiadomień w czasie rzeczywistym. Jest bardziej zaawansowany niż POP3, umożliwiając synchronizację między urządzeniami.                                                                   | 143 (nieszyfrowany), 993 (IMAPS)    | TCP                                        | Klienty pocztowe jak Outlook, Thunderbird; serwery jak Gmail.                               |
| POP3 (Post Office Protocol version 3)   | Protokół do pobierania e-maili z serwera na urządzenie lokalne. Jest prosty, obsługuje komendy jak RETR (pobierz), DELE (usuń). Po pobraniu wiadomości są usuwane z serwera (domyślnie), co czyni go mniej elastycznym niż IMAP.                                                                                                                                   | 110 (nieszyfrowany), 995 (POP3S)    | TCP                                        | Starsze klienty pocztowe; mniej używany dziś ze względu na mobilność.                       |
| SMTP (Simple Mail Transfer Protocol)    | Protokół do wysyłania e-maili między serwerami lub od klienta do serwera. Obsługuje uwierzytelnianie (np. STARTTLS), załączniki (MIME). Nie obsługuje pobierania – do tego służy POP3/IMAP. Jest podatny na spam, dlatego wymaga filtrów.                                                                                                                          | 25 (nieszyfrowany), 465/587 (SMTPS) | TCP                                        | Wysyłanie e-maili; serwery jak Postfix, Sendmail.                                           |
| SSH (Secure Shell)                      | Protokół do bezpiecznego zdalnego dostępu do systemów. Zapewnia szyfrowane połączenie, uwierzytelnianie kluczami publicznymi/prywatnymi, tunelowanie portów. Jest następcą Telnetu, obsługuje SFTP dla transferu plików.                                                                                                                                           | 22                                  | TCP                                        | Administracja serwerami Linux; narzędzia jak PuTTY, OpenSSH.                                |
| Telnet                                  | Starszy protokół do zdalnego dostępu tekstowego. Przesyła dane w plaintext, co czyni go niebezpiecznym (łatwy do podsłuchu). Obsługuje proste komendy terminalowe, ale jest rzadko używany dziś ze względu na brak bezpieczeństwa.                                                                                                                                 | 23                                  | TCP                                        | Testowanie połączeń; zastąpiony przez SSH.                                                  |

Te protokoły są podstawą większości aplikacji internetowych i sieciowych. Na przykład, przeglądarka używa HTTP/HTTPS do pobierania stron, DNS do resolvowania adresów, a e-mail – kombinacji SMTP, IMAP/POP3. W praktyce, wiele aplikacji łączy kilka protokołów (np. webmail używa HTTPS + SMTP/IMAP).
## 2. Warstwa Transportu w modelu TCP/IP.
Warstwa transportowa (ang. Transport Layer) to trzecia warstwa w modelu TCP/IP (licząc od dołu). Jest to warstwa end-to-end – oznacza, że komunikuje się bezpośrednio między dwoma hostami (komputerami, serwerami, telefonami), niezależnie od tego, ile routerów jest po drodze. Jej głównym zadaniem jest zapewnienie niezawodnej (lub możliwie szybkiej) dostawy danych pomiędzy aplikacjami działającymi na tych hostach.
W modelu TCP/IP warstwa transportowa odpowiada w przybliżeniu warstwie 4 (transportowej) modelu OSI, ale jest nieco szersza w zakresie funkcji.
Główne zadania warstwy transportowej

Multipleksowanie i demultipleksowanie
1. Dzięki numerom portów (0–65535) wiele aplikacji na jednym hoście może jednocześnie korzystać z sieci.
2. Nadawca wskazuje port docelowy (np. 80 dla HTTP), odbiorca na podstawie portu przekazuje dane do właściwej aplikacji.
Segmentacja i rekonstrukcja danych
3. Dane z warstwy aplikacji są dzielone na mniejsze jednostki (segmenty w TCP, datagramy w UDP), które mogą być przesyłane przez sieć.
Kontrola przepływu (flow control)
4. Zapobiega zalewaniu wolniejszego odbiorcy zbyt dużą ilością danych (TCP używa okna odbiorczego – sliding window).
Kontrola błędów i niezawodność
5. Wykrywanie i poprawianie błędów oraz utraconych pakietów (tylko TCP).
Kontrola przeciążenia (congestion control)
6. TCP dynamicznie dostosowuje szybkość wysyłania, aby nie przeciążać sieci.
Utrzymywanie połączenia lub tryb bezpołączeniowy
7. TCP: połączenie z trójfazowym handshake’em i uporządkowanym zakończeniem.
8. UDP: bezpołączeniowy, „wystrzel i zapomnij”.

### Szczegółowe działanie TCP – najważniejsze mechanizmy

1. __Trójfazowy handshake (3-way handshake)__  
SYN → SYN-ACK → ACK
Ustanawia połączenie i synchronizuje numery sekwencyjne.
2. __Numery sekwencyjne i potwierdzenia (Sequence & Acknowledgment Numbers)__  
Każdy bajt danych ma swój numer. Odbiorca potwierdza, które bajty otrzymał prawidłowo.
3. __Okno odbiorcze (Receiving Window)__  
Odbiorca mówi: „Mam miejsce na kolejne X bajtów” – nadawca nie wyśle więcej.
4. __Algorytmy kontroli przeciążenia (najnowsze systemy – Cubic, BBR)__  
– Slow Start
– Congestion Avoidance
– Fast Retransmit (3 duplicate ACK)
– Fast Recovery
– Selective Acknowledgment (SACK) – pozwala potwierdzić nie tylko ciągły zakres
5. __Zakończenie połączenia (4-way handshake)__  
FIN → ACK → FIN → ACK (half-close możliwe)

UDP – kiedy brak mechanizmów jest zaletą
UDP jest wybierany świadomie tam, gdzie:

Liczy się minimalne opóźnienie (gry online – lepiej stracić jeden pakiet niż czekać na retransmisję)
Strumieniowanie wideo/audio (krótkotrwałe zgubienie pakietu jest mniej dokuczliwe niż buforowanie)
Zapytania DNS (większość to małe pakiety <512 B, odpowiedź przychodzi szybko)
IoT i urządzenia o małej mocy (oszczędzanie baterii i procesora)

Nowoczesne protokoły „nad UDP” (QUIC, WebRTC, SRT) same implementują brakujące mechanizmy TCP (szyfrowanie, niezawodność, kontrolę przeciążenia), ale robią to bardziej efektywnie niż klasyczny TCP.

|    Zakres   |                                Opis                                |              Przykłady             |
|:-----------:|:------------------------------------------------------------------:|:----------------------------------:|
| 0–1023      | Well-Known Ports (zarezerwowane, wymagają uprawnień root/admin)    | 22 SSH, 80 HTTP, 443 HTTPS, 53 DNS |
| 1024–49151  | Registered Ports (zarejestrowane przez IANA dla konkretnych usług) | 3306 MySQL, 5432 PostgreSQL        |
| 49152–65535 | Ephemeral/Dynamic (przydzielane tymczasowo klientom)               | Port źródłowy przeglądarki         |

|            Zastosowanie            |                 Preferowany protokół                |                                    Dlaczego?                                   |
|:----------------------------------:|:---------------------------------------------------:|:------------------------------------------------------------------------------:|
| Strony internetowe (HTTP/3)        | QUIC (nad UDP)                                      | Szybsze nawiązywanie połączenia, multipleksowanie, mobilność (zmiana Wi-Fi/4G) |
| Klasyczne strony i API             | TCP + TLS                                           | Nadal dominuje w starszych systemach                                           |
| Streaming wideo (Netflix, YouTube) | UDP (DASH/HLS) + częściowa niezawodność w aplikacji |                                                                                |
| Gry online                         | UDP + własne protokoły                              | Minimalne opóźnienia                                                           |
| VoIP / wideorozmowy                | UDP (WebRTC, SRTP)                                  | Niskie latency                                                                 |
| Przesyłanie plików, e-mail         | TCP                                                 | 100% niezawodność wymagana                                                     |
## 3. Warstwa Internetowa.

Warstwa internetowa (czasami nazywana też warstwą sieciową) to druga warstwa w klasycznym modelu TCP/IP (licząc od dołu). Jest to najważniejsza warstwa z punktu widzenia samego istnienia Internetu jako globalnej, między-sieciowej struktury.
W modelu TCP/IP odpowiada ona w przybliżeniu warstwie 3 (Network Layer) modelu OSI, ale ma kilka charakterystycznych różnic w zakresie i filozofii projektowania.

|             Zadanie             |                                       Opis                                       |         Kluczowe protokoły/mechanizmy         |
|:-------------------------------:|:--------------------------------------------------------------------------------:|:---------------------------------------------:|
| Adresowanie logiczne            | Nadawanie unikalnych adresów w skali globalnej (IP)                              | IPv4, IPv6                                    |
| Pakietowanie (encapsulation)    | Tworzenie pakietów IP z segmentów/danych z warstwy transportowej                 | Nagłówek IP                                   |
| Routing między sieciami         | Decyzja, którędy przesyłać pakiety pomiędzy różnymi sieciami                     | Protokoły routingu (BGP, OSPF, IS-IS, RIP…)   |
| Fragmentacja i defragmentacja   | Rozbijanie zbyt dużych pakietów na mniejsze fragmenty i składanie ich z powrotem | Pole Fragment Offset, Identification, MF flag |
| Najlepszy wysiłek (best-effort) | Brak gwarancji dostarczenia, kolejności, braku duplikatów czy integralności      | Charakterystyczna cecha IP                    |
| Time To Live (TTL) / Hop Limit  | Ochrona przed nieskończonymi pętlami routingu                                    | Pole TTL (IPv4) / Hop Limit (IPv6)            |
| Podstawowa diagnostyka          | Narzędzia do testowania osiągalności i trasy                                     | ICMP, ICMPv6, traceroute, ping                |

### Najważniejsze protokoły warstwy internetowej (stan na 2026 r.)
| Protokół |                                          Opis                                         |            Status w 2026 roku            |           Uwagi / zastosowania współczesne           |
|:--------:|:-------------------------------------------------------------------------------------:|:----------------------------------------:|:----------------------------------------------------:|
| IPv4     | Podstawowy protokół adresowania 32-bitowego (ok. 4,3 mld adresów)                     | Nadal ~55–65% ruchu globalnego           | NAT jest wszechobecny, końcówka puli adresów 2011    |
| IPv6     | 128-bitowe adresowanie (~340 undecylionów adresów), wbudowane IPsec, autokonfiguracja | ~42–48% ruchu globalnego (szybki wzrost) | Obowiązkowy w nowych urządzeniach 5G, IoT, chmurze   |
| ICMP     | Internet Control Message Protocol – komunikaty diagnostyczne i błędy                  | Niezbędny                                | Ping, traceroute, Path MTU Discovery                 |
| ICMPv6   | Rozszerzona wersja ICMP dla IPv6 + bardzo ważny Neighbor Discovery Protocol (NDP)     | Obowiązkowy w IPv6                       | Zamienia ARP, Router Discovery, MLD (multicast)      |
| IPsec    | Zestaw protokołów do szyfrowania i uwierzytelniania na poziomie IP                    | Coraz powszechniejszy                    | Często używany w VPN, ale w 2026 częściej QUIC/TLS   |
| IGMP/MLD | Zarządzanie członkostwem w grupach multicastowych (IPv4 → IGMP, IPv6 → MLD)           | Używane w IPTV, streaming multicast      | Coraz rzadziej w dużych serwisach (przewaga unicast) |

#### Kluczowe różnice między IPv4 a IPv6 (najważniejsze w 2026 r.)
## 4. Warstwa Dostępu do Sieci.

Jest to warstwa na poziomie najniższym, i opiera się o bazowe protokoły przekazu danych. Do standardowych protokołów należeć będzie tutaj ethernet czy wi-fi.
Cytując chata : Odpowiada ona za fizyczne przesyłanie bitów przez media transmisyjne oraz adresowanie sprzętowe (MAC).

Do protokołów tej warstwy zaliczają się przede wszystkim : 
- Ethernet (IEEE 802.3): Najpopularniejszy standard dla sieci przewodowych LAN.
- Wi-Fi (IEEE 802.11): Standard dla bezprzewodowych sieci lokalnych (WLAN).
- PPP (Point-to-Point Protocol): Używany do bezpośredniego połączenia dwóch węzłów (np. przez modem).
- ARP (Address Resolution Protocol): Choć technicznie działa "pomiędzy" warstwami, często przypisuje się go tutaj, ponieważ tłumaczy adresy IP na adresy fizyczne MAC.
- Token Ring / FDDI: Starsze, obecnie rzadziej spotykane standardy przesyłu danych.
- DSL / Frame Relay / ATM: Technologie szerokopasmowego dostępu do sieci.

### Czy Zigbee i Bluetooth należą do tej warstwy?
Odpowiedź brzmi: Tak, ale z pewnym zastrzeżeniem.

Z punktu widzenia modelu TCP/IP, Zigbee oraz Bluetooth pełnią tę samą rolę co Wi-Fi czy Ethernet – dostarczają fizyczne medium i sposób adresowania urządzeń w zasięgu bezpośrednim.

- Bluetooth (IEEE 802.15.1): Obsługuje warstwę fizyczną i łącza danych. Jeśli Twój telefon łączy się z Internetem przez Bluetooth (tzw. tethering), to Bluetooth staje się protokołem warstwy dostępu do sieci dla całego stosu TCP/IP.

- Zigbee (IEEE 802.15.4): Sytuacja jest tu nieco bardziej złożona. Sam protokół Zigbee jest kompletnym "stosem" (ma własne warstwy sieci i aplikacji, które nie są kompatybilne z IP). Jednak istnieją rozszerzenia, takie jak Zigbee IP lub 6LoWPAN, które pozwalają na przesyłanie pakietów IPv6 przez radiową warstwę Zigbee. W takim scenariuszu Zigbee (a konkretnie standard 802.15.4) jest traktowane jako warstwa dostępu do sieci.

Ważna uwaga: Zigbee i Bluetooth same w sobie są osobnymi architekturami. Często mówi się, że są to protokoły "zamiast" TCP/IP w małych urządzeniach IoT, ponieważ standardowe TCP/IP jest dla nich zbyt "ciężkie" (wymaga dużo energii i pamięci).

# Model Iso / OSI

### Warstwa 7: aplikacji
Warstwa aplikacji jest warstwą najwyższą, zajmuje się specyfikacją interfejsu, który wykorzystują aplikacje do przesyłania danych do sieci (poprzez kolejne warstwy modelu ISO/OSI). W przypadku sieci komputerowych aplikacje są zwykle procesami uruchomionymi na odległych hostach. Interfejs udostępniający programistom usługi dostarczane przez warstwę aplikacji opiera się na obiektach nazywanych gniazdami (ang. socket).

Jeżeli użytkownik posługuje się oprogramowaniem działającym w architekturze klient-serwer, zwykle po jego stronie znajduje się klient, a serwer działa na maszynie podłączonej do sieci świadczącej usługi równocześnie wielu klientom. Zarówno serwer, jak i klient znajdują się w warstwie aplikacji. Komunikacja nigdy nie odbywa się bezpośrednio między tymi programami. Kiedy klient chce przesłać żądanie do serwera, przekazuje komunikat w dół do warstw niższych, które fizycznie przesyłają go do odpowiedniej maszyny, gdzie informacje ponownie wędrują w górę i są ostatecznie odbierane przez serwer. Jednocześnie zapewnia interfejs między aplikacjami, których używamy, a siecią (umożliwia komunikację).

### Warstwa 6: prezentacji
Podczas ruchu w dół zadaniem warstwy prezentacji jest przetworzenie danych od aplikacji do postaci kanonicznej (ang. canonical representation) zgodnej ze specyfikacją OSI-RM, dzięki czemu niższe warstwy zawsze otrzymują dane w tym samym formacie. Kiedy informacje płyną w górę, warstwa prezentacji tłumaczy format otrzymywanych danych na zgodny z wewnętrzną reprezentacją systemu docelowego. Wynika to ze zróżnicowania systemów komputerowych, które mogą w różny sposób interpretować te same dane. Dla przykładu bity w bajcie danych w niektórych procesorach są interpretowane w odwrotnej kolejności niż w innych. Warstwa ta odpowiada za kodowanie i konwersję danych oraz za kompresję / dekompresję; szyfrowanie / deszyfrowanie. Warstwa prezentacji obsługuje np. MPEG, JPG, GIF.

### Warstwa 5: sesji
Warstwa sesji otrzymuje od różnych aplikacji dane, które muszą zostać odpowiednio zsynchronizowane. Synchronizacja występuje między warstwami sesji systemu nadawcy i odbiorcy. Warstwa sesji „wie”, która aplikacja łączy się z którą, dzięki czemu może zapewnić właściwy kierunek przepływu danych – nadzoruje połączenie. Wznawia je po przerwaniu.

### Warstwa 4: transportowa
Warstwa transportowa segmentuje dane oraz składa je w tzw. strumień. Warstwa ta zapewnia całościowe połączenie między stacjami: źródłową oraz docelową, które obejmuje całą drogę transmisji. Następuje tutaj podział danych na części, które są kolejno indeksowane i wysyłane do docelowej stacji. Na poziomie tej warstwy do transmisji danych wykorzystuje się dwa protokoły TCP (ang. Transmission Control Protocol) oraz UDP (ang. User Datagram Protocol). W przypadku gdy do transmisji danych wykorzystany jest protokół TCP stacja docelowa po odebraniu segmentu wysyła potwierdzenie odbioru. W wyniku niedotarcia któregoś z segmentów stacja docelowa ma prawo zlecić ponowną jego wysyłkę (kontrola błędów transportu). W przeciwieństwie do protokołu TCP w protokole UDP nie stosuje się potwierdzeń. Protokół UDP z racji konieczności transmisji mniejszej ilości danych zazwyczaj jest szybszy od protokołu TCP, jednakże nie gwarantuje dostarczenia pakietu. Oba protokoły warstwy transportowej stosują kontrolę integralności pakietów, a pakiety zawierające błędy są odrzucane.

### Warstwa 3: sieciowa
Warstwa sieciowa jako jedyna dysponuje wiedzą dotyczącą fizycznej topologii sieci. Rozpoznaje, jakie drogi łączą poszczególne komputery (trasowanie) i decyduje, ile informacji należy przesłać jednym z połączeń, a ile innym. Jeżeli danych do przesłania jest zbyt wiele, to warstwa sieciowa po prostu je ignoruje. Nie musi zapewniać pewności transmisji, więc w razie błędu pomija niepoprawne pakiety danych. Standardowa paczka danych czasami oznaczana jest jako NPDU (ang. Network Protocol Data Unit). Nie znajdują się w nim żadne użyteczne dla użytkowników dane. Jedyne jego zadanie, to zapewnienie sprawnej łączności między bardzo odległymi punktami sieci. Routery są podstawą budowy rozległych sieci informatycznych takich jak Internet, bo potrafią odnaleźć najlepszą drogę do przekazania informacji. Warstwa sieciowa podczas ruchu w dół umieszcza dane wewnątrz pakietów zrozumiałych dla warstw niższych (kapsułkowanie). Jednocześnie warstwa sieci używa czterech procesów (adresowanie, enkapsulacja, routing, dekapsulacja). Protokoły warstwy sieci to: (IPv4, IPv6, ICMP, NOVELL IPX, APPLE TALK, CLNS/DECN itd.).

### Warstwa 2: łącza danych
Warstwa łącza danych jest czasami nazywana warstwą liniową lub kanałową. Ma ona nadzorować jakość przekazywanych informacji. Nadzór ten dotyczy wyłącznie warstwy niższej. Warstwa łącza danych ma możliwość zmiany parametrów pracy warstwy fizycznej, tak aby obniżyć liczbę pojawiających się podczas przekazu błędów. Zajmuje się pakowaniem danych w ramki i wysyłaniem do warstwy fizycznej. Rozpoznaje błędy związane z gubieniem pakietów oraz uszkodzeniem ramek i zajmuje się ich naprawą. Podczas ruchu w dół w warstwie łącza danych zachodzi enkapsulacja pakietów z warstwy sieciowej tak, aby uzyskać ramki zgodne ze standardem. Czasami są one oznaczane jako LPDU (ang. Link Protocol Data Unit).

Ramka danych przeważnie składa się z:

- ID odbiorcy – najczęściej adres MAC stacji docelowej lub bramy domyślnej,
- ID nadawcy – najczęściej adres MAC stacji źródłowej,
informacja sterująca – zawiera dane o typie ramki, trasowaniu, segmentacji itp.,
- CRC (ang. Cyclic Redundancy Check) – kod kontroli cyklicznej – odpowiada za korekcję błędów i weryfikację poprawności danych otrzymywanych przez stację docelową.
- Warstwa łącza danych dzieli się na dwie podwarstwy:

  - LLC (ang. logical link control) – sterowania łączem danych – kontroluje poprawność transmisji i współpracuje przede wszystkim z warstwą sieciową w obsłudze usług połączeniowych i bezpołączeniowych.
  - MAC (ang. media access control) – sterowania dostępem do nośnika – zapewnia dostęp do nośnika sieci lokalnej i współpracuje przede wszystkim z warstwą fizyczną.

### Warstwa 1: fizyczna
Fundamentem, na którym zbudowany jest model referencyjny OSI, jest jego warstwa fizyczna. Określa ona wszystkie składniki sieci niezbędne do obsługi elektrycznego, optycznego, radiowego wysyłania i odbierania sygnałów. Warstwa fizyczna składa się z czterech obszarów funkcjonalnych:

- mechanicznego,
- elektrycznego,
- funkcjonalnego,
- proceduralnego.
  
Wspólnie obejmują one wszystkie mechanizmy potrzebne do obsługi transmisji danych, takie jak techniki sygnalizacyjne, napięcie elektryczne powodujące przepływ prądu elektrycznego przenoszącego sygnał, rodzaje nośników i odpowiadające im właściwości impedancji, elektroniczne składniki kart sieciowych, a nawet fizyczny kształt złącza używanego do terminacji nośnika.

Warstwa fizyczna przesyła i odbiera sygnały zaadresowane dla wszystkich protokołów jej stosu oraz aplikacji, które je wykorzystują. Musi ona więc wykonywać kilka istotnych funkcji – w szczególności:

Aby móc nadawać dane, musi ona:

- zamieniać dane znajdujące się w ramkach na strumienie binarne,
- wykonywać taką metodę dostępu do nośnika, jakiej żąda warstwa łącza danych,
- przesyłać ramki danych szeregowo (czyli bit po bicie) w postaci strumieni binarnych.  
  
W celu odbierania danych konieczne jest natomiast:  
- oczekiwanie na transmisje przychodzące do urządzenia hosta i do niego zaadresowane,
- odbiór odpowiednio zaadresowanych strumieni,
- przesyłanie binarnych strumieni do warstwy łącza danych w celu złożenia ich z powrotem w ramki.
Lista ta, jak widać, nie obejmuje żadnych sposobów weryfikowania integralności danych. Warstwa fizyczna nie posiada bowiem mechanizmu służącego rozpoznawaniu znaczenia wysyłanych, jak też otrzymywanych danych. Służy wyłącznie przesyłaniu logicznych zer i jedynek.

Warstwa fizyczna, w postaci określonej przez Model Referencyjny OSI, składa się ze wszystkich procesów, mechanizmów, elektroniki oraz protokołów, które potrzebne są urządzeniu obliczającemu w celu wysłania i odbierania binarnych strumieni danych. W specyfikacji warstwy fizycznej technologii LAN zamieszczone są oczekiwania odnośnie do wydajności nośnika łączącego komunikujące się ze sobą urządzenia. Model jednak nie określa samego rodzaju nośnika.

# Porównanie Modeli Warstw !!! 
![Porównanie Modeli](https://www.networkstraining.com/wp-content/uploads/2022/09/osi-tcpip.png),
oraz bardziej precyzyjne porównanie: 
![Porównanie Modeli 2](https://networkinterview.com/wp-content/uploads/2021/07/TCP-IP-MODEL-VS-OSI-MODEL-TABLE.jpg)