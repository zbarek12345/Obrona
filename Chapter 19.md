### Technologie zapór ogniowych (Firewalls)

Zapora ogniowa (firewall) to urządzenie bezpieczeństwa sieciowego lub oprogramowanie, które monitoruje i kontroluje ruch sieciowy na podstawie zdefiniowanych reguł bezpieczeństwa. Jej głównym zadaniem jest blokowanie nieautoryzowanego dostępu oraz zezwalanie na ruch zgodny z polityką bezpieczeństwa. Firewall działa jako bariera między zaufaną siecią wewnętrzną a niezaufanymi sieciami zewnętrznymi (np. Internetem).

#### Główne typy zapór ogniowych

1. **Filtrujące pakiety (Packet Filtering Firewalls)**
    - Najprostszy i najstarszy typ.
    - Analizują nagłówki pakietów IP (adres źródłowy/docelowy, porty, protokół – np. TCP/UDP).
    - Decydują o zezwoleniu lub odrzuceniu pakietu na podstawie statycznych reguł (ACL – Access Control Lists).
    - Zalety: szybkie, niskie zużycie zasobów.
    - Wady: nie analizują zawartości pakietów, nie śledzą stanu połączenia, podatne na spoofing i ataki wykorzystujące fragmentację.

2. **Stanowe zapory ogniowe (Stateful Inspection Firewalls)**
    - Rozwinięcie filtrów pakietowych.
    - Śledzą stan połączeń (tabela stanów – state table): nowe, ustanowione, powiązane (np. FTP wymaga dodatkowych portów danych).
    - Pozwalają na ruch zwrotny tylko dla ustanowionych połączeń.
    - Zalety: skuteczniejsze przeciwko spoofingowi i atakom typu SYN flood.
    - Są standardem w większości nowoczesnych firewalli.

3. **Zapory aplikacyjne / proxy (Application-Level Gateways / Proxy Firewalls)**
    - Działają na warstwie aplikacji (OSI layer 7).
    - Przechwytują ruch, kończą połączenie po jednej stronie i otwierają nowe po drugiej (proxy).
    - Analizują zawartość (np. komendy HTTP, SMTP).
    - Zalety: bardzo dokładna kontrola, ukrywanie struktury sieci wewnętrznej.
    - Wady: wyższe opóźnienia, większe zużycie zasobów, konieczność konfiguracji dla każdej aplikacji.

4. **Zapory nowej generacji (Next-Generation Firewalls – NGFW)**
    - Łączą funkcje poprzednich typów z dodatkowymi możliwościami:
        - Głęboka inspekcja pakietów (Deep Packet Inspection – DPI).
        - Integracja z systemami wykrywania/prewencji włamań (IPS).
        - Kontrola aplikacji (rozpoznawanie np. Facebooka nawet na niestandardowych portach).
        - Filtrowanie URL, ochrona przed malware, SSL/TLS decryption.
        - Często oparte na inteligencji zagrożeń (threat intelligence feeds).
    - Przykłady producentów: Palo Alto Networks, Fortinet, Check Point, Cisco Firepower.

### Systemy wykrywania włamań (Intrusion Detection Systems – IDS)

System wykrywania włamań (IDS) to rozwiązanie monitorujące sieć lub hosty w poszukiwaniu podejrzanej lub złośliwej aktywności. W przeciwieństwie do firewalla, który aktywnie blokuje ruch, IDS głównie **wykrywa** i **alarmuje** (loguje, wysyła powiadomienia). Nie modyfikuje ruchu sieciowego (chyba że jest połączony z IPS).

#### Główne typy IDS

1. **Sieciowe IDS (Network-based IDS – NIDS)**
    - Monitorują ruch sieciowy w kluczowych punktach (np. na switchu w trybie mirror/SPAN lub inline).
    - Analizują przechwycone pakiety.
    - Przykłady: Snort, Suricata, Zeek (dawniej Bro).

2. **Hostowe IDS (Host-based IDS – HIDS)**
    - Instalowane na pojedynczych serwerach/komputerach.
    - Monitorują aktywność systemu: pliki, logi systemowe, procesy, integralność plików (file integrity monitoring).
    - Przykłady: OSSEC, Tripwire, Wazuh.

3. **Hybrydowe** – łączą NIDS i HIDS.

#### Metody wykrywania

1. **Oparte na sygnaturach (Signature-based / Rule-based)**
    - Porównują obserwowany ruch/zachowanie z bazą znanych sygnatur ataków (podobnie jak antywirus).
    - Zalety: bardzo dokładne dla znanych zagrożeń, niska liczba fałszywych alarmów.
    - Wady: bezużyteczne przeciwko nowym (zero-day) atakom.

2. **Oparte na anomalii (Anomaly-based / Behavior-based)**
    - Tworzą model „normalnego” zachowania (baseline) przy użyciu uczenia maszynowego/statystyki.
    - Alarmują przy odchyleniach (np. nietypowy duży transfer danych w nocy).
    - Zalety: wykrywa nieznane ataki.
    - Wady: więcej fałszywych alarmów (false positives), wymaga okresu nauki.

3. **Analiza stanu protokołu (Stateful Protocol Analysis)**
    - Porównuje obserwowane użycie protokołów z ich specyfikacją RFC.
    - Wykrywa np. nieprawidłowe sekwencje komend.

### Systemy prewencji włamań (Intrusion Prevention Systems – IPS)

Często mylone z IDS – IPS to IDS z możliwością aktywnego blokowania (działa inline i może odrzucać pakiety lub zrywać połączenia). Wiele nowoczesnych rozwiązań (np. w NGFW) łączy IDS/IPS.

### Porównanie i współpraca

- **Firewall** – zapobiega (prewencja) poprzez filtrowanie na podstawie reguł.
- **IDS** – wykrywa (detekcja) i alarmuje, ale nie blokuje (chyba że IPS).

W praktyce często działają razem:
- Firewall jako pierwsza linia obrony (blokuje oczywiste zagrożenia).
- IDS/IPS jako druga linia (wykrywa to, co przeszło przez firewall).

Współczesne urządzenia UTM (Unified Threat Management) lub NGFW integrują obie technologie wraz z antywirusem, filtrowaniem treści itp.

Jeśli potrzebujesz bardziej szczegółowego opisu konkretnego typu, przykładów konfiguracji lub aktualnych trendów (np. firewalli chmurowych jak AWS WAF czy Zero Trust), daj znać!