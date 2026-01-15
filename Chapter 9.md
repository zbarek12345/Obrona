# Programowalne scalone układy cyfrowe PLD, CPLD oraz FPGA
Programowalne układy logiczne (z ang. Programmable Logic Devices – PLD) to rewolucyjne rozwiązanie w świecie elektroniki. W przeciwieństwie do standardowych układów scalonych (jak procesory czy bramki logiczne serii 7400), ich funkcja nie jest ustalona na etapie produkcji, lecz definiowana przez projektanta za pomocą kodu (VHDL, Verilog).

Możemy je podzielić na trzy główne kategorie, które ewoluowały wraz ze wzrostem złożoności projektów.

## 1. Proste układy PLD (Programmable Logic Devices)
To najstarsza i najprostsza grupa układów, do której zaliczamy m.in. PAL (Programmable Array Logic) oraz GAL (Generic Array Logic).

- Budowa: Opierają się na matrycy bramek AND oraz OR. W układach PAL matryca AND jest programowalna, a OR stała.

- Zastosowanie: Realizacja prostych funkcji logicznych, zastępowanie kilku pojedynczych układów scalonych na płytce (tzw. "glue logic").

- Skala: Zawierają od kilkunastu do kilkudziesięciu bramek logicznych.

## 2. Układy CPLD (Complex Programmable Logic Devices)
CPLD to naturalna ewolucja układów PLD. Można je sobie wyobrazić jako wiele małych układów PAL umieszczonych w jednej obudowie i połączonych wspólną matrycą połączeń.

- Budowa: Składają się z makrokomórek (Macrocells), które zawierają bramki logiczne oraz przerzutnik (do zapamiętywania stanów).

- Pamięć nieulotna: Większość CPLD posiada wbudowaną pamięć typu Flash. Oznacza to, że układ po włączeniu zasilania jest natychmiast gotowy do pracy – nie musi pobierać konfiguracji z zewnątrz.

- Charakterystyka: Cechują się bardzo przewidywalnym czasem propagacji sygnału (wiemy dokładnie, ile nanosekund zajmie operacja), co jest kluczowe w szybkich układach sterujących.

## 3. Układy FPGA (Field Programmable Gate Array)
FPGA to najbardziej zaawansowane układy z tej rodziny, oferujące ogromną moc obliczeniową i elastyczność.

- Budowa: Zamiast matrycy bramek, FPGA opiera się na tzw. blokach logicznych (CLB – Configurable Logic Blocks). Sercem każdego bloku jest tablica LUT (Look-Up Table), która emuluje funkcje logiczne, działając jak mała pamięć RAM.

- Pamięć ulotna: FPGA zazwyczaj bazują na technologii SRAM. Oznacza to, że po odłączeniu zasilania "zapominają" swoją konfigurację. Dlatego na płytce obok FPGA zawsze znajduje się mała pamięć zewnętrzna (np. EEPROM/Flash), z której układ ładuje program przy starcie.

- Zasoby dodatkowe: Nowoczesne FPGA posiadają wbudowane bloki dedykowane, takie jak:

- Szybkie mnożniki i jednostki DSP.

- Bloki pamięci RAM.

- Gotowe rdzenie procesorów (np. ARM).

## Porównanie

| Cecha                 | CPLD                             | FPGA                                          |
|-----------------------|----------------------------------|-----------------------------------------------|
| Architektura          | Makrokomórki (bloki logiczne)    | Tablice LUT (pamięć)                          |
| Gęstość upakowania    | Mała / Średnia                   | Bardzo duża (miliony bramek)                  |
| Pobór prądu           | Niski                            | Wyższy (szczególnie przy dużych taktowaniach) |
| Konfiguracja          | Nieulotna (Flash)                | Ulotna (wymaga zewnętrznej pamięci)           |
| Przewidywalność czasu | Bardzo wysoka (deterministyczna) | Zależna od routingu (skomplikowana)           |