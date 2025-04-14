
## 🛰 Manifest systemu M.A.R.S  
**Modular Autonomous Resilient System**

> _Nie umrę. Nie zamilknę. Będę działać tak długo, jak choć jeden bit logiki pozostanie aktywny._

M.A.R.S to nie tylko system elektroniczny. To **samodzielna istota techniczna**, stworzona jako wysłannik człowieka do miejsc, gdzie nadzór, zasilanie i wsparcie zawodzą. To duch eksploracji, zaklęty w układach scalonych. To odpowiedź na pytanie: *czy system może przetrwać sam?*

Tak jak sondy Voyager, które przekroczyły granice heliosfery — działając daleko poza zakładane możliwości — tak i M.A.R.S ma służyć **nieprzerwanie**, nawet jeśli zostanie samotny, uszkodzony, lub zapomniany.

System ten został zaprojektowany z myślą o **niezależności, samonaprawie i decyzyjności**, w oparciu o zasady:
- Minimalne zależności zewnętrzne
- Redundancja sprzętowa i programowa
- Modułowość i rekonfigurowalność
- Ciągłe monitorowanie własnego stanu
- Praca degradacyjna zamiast zatrzymania
- Autonomia energetyczna i komunikacyjna
- Możliwość naprawy, rekonfiguracji i rozszerzania przez operatora – nawet zdalnie

M.A.R.S jest manifestacją **nieposkromionego ducha ludzkiej inżynierii**: odpornego, elastycznego, zawsze dzielącego się zdobytą wiedzą — dopóki tylko jest w nim iskra.

![[8b5a5c3f-2fe9-43c2-a14b-1b78f91e9d35.png]]


>_INVICTUS ANIMUS, ULTRA FINEM RERUM_



## Założenia główne projektu M.A.R.S
1. Modularna, skalowalna platforma sprzętowo-programowa do zdalnego sterowania, autonomicznego wykonywania zadań i wielokanałowej akwizycji danych z czujników. System wspiera lokalizację w czasie rzeczywistym ([[GNSS]]/[[INS]]/[[RTK]]), komunikację dwukierunkową (LTE/NB-IoT/LoRa), oraz analizę i przesył danych do systemów nadrzędnych ([[MQTT]]/[[REST]]/[[WebSocket]]).
2. Możliwość pracy w trybie półautonomicznym (operator nadzorujący) lub całkowicie autonomicznym, z lokalnym podejmowaniem decyzji na podstawie danych z sensorów i logiki stanu. System przystosowany do pracy w środowiskach o ograniczonej infrastrukturze komunikacyjnej, z zapewnieniem odporności na zakłócenia (watchdog, fallback logic, redundantne kanały komunikacji).
3. Wbudowany system autodiagnostyki i raportowania stanu komponentów sprzętowych i programowych, z rejestrowaniem zdarzeń w pamięci lokalnej oraz możliwością zdalnego monitoringu. Obsługa mechanizmów watchdog, logowania błędów, detekcji anomalii i transmisji komunikatów diagnostycznych ([[MQTT]]/syslog/[[JSON]]-[[REST]]), z opcjonalnym wykorzystaniem LoRa beaconów i wsparciem dla sieci LoRaWAN do niskoenergetycznej transmisji danych diagnostycznych.
4. Obsługa elastycznego zasilania z wykorzystaniem dedykowanego układu zarządzania energią ([[PMIC]]), umożliwiającego pracę z szerokim zakresem napięć wejściowych (np. 5–24 V DC), obsługę ładowania akumulatorów Li-Ion/LiFePO₄, detekcję źródła zasilania, monitorowanie napięć/prądów oraz tryby oszczędzania energii (deep sleep, standby). Możliwa integracja z USB-C (PD), PoE lub innymi źródłami zasilania zewnętrznego.
5. Wbudowane mechanizmy zapewnienia ciągłości działania systemu poprzez redundancję i logikę awaryjną na poziomie komunikacji (fallback LTE/SMS/LoRa), zasilania (automatyczne przełączanie źródeł przez [[PMIC]]), software’u (watchdog, auto[[REST]]art, tryby degradacyjne), oraz architektury sprzętowej (modularność, rekonfigurowalność, backup MCU z własnym zasilaniem). System wspiera podstawową transmisję telemetrii (raporty stanu, heartbeat) nawet przy minimalnym paśmie transmisji, z logiką sondy kosmicznej – podejmując autonomiczne decyzje w razie braku łączności.
6. Projekt realizowany zgodnie z zasadami otwartego hardware i software, z pełną dokumentacją sprzętową (schematy, PCB, BOM) w formatach open-source (np. KiCad) i kodem źródłowym oprogramowania (Firmware/Tooling) na licencjach typu MIT/GPL. Repozytoria dostępne publicznie z możliwością forku, modyfikacji i niezależnego audytu.
7. Projekt nie jest ukierunkowany na finalny, komercyjny produkt, lecz na nieprzerwaną fazę badawczo-rozwojową (R&D), umożliwiającą swobodne eksperymentowanie z architekturą sprzętową i programową, inkrementalne wprowadzanie zmian oraz testowanie koncepcji bez ograniczeń cyklem produkcyjnym.
8. Preferowane wykorzystanie, adaptacja i modyfikacja istniejących rozwiązań open-source, przy każdorazowej ocenie kosztów wdrożenia względem funkcjonalności i czasu realizacji (czas vs. wartość).
9. Brak zależności od zewnętrznych, zamkniętych ekosystemów – projekt musi umożliwiać pełną kontrolę nad kodem źródłowym, sprzętem i procesem rozwoju. Wszystkie warstwy systemu muszą być możliwe do zbudowania i uruchomienia lokalnie.
10. Projekt pełni funkcję edukacyjną – rozwój kompetencji w zakresie tworzenia firmware’u i projektowania PCB oraz eksperymentalna implementacja mikro-AI (TinyML) w warunkach ograniczonej infrastruktury.
11. Efektywność kosztowa – komponenty dobierane na podstawie stosunku możliwości do ceny.

12. System zaprojektowany jako mobilny, gotowy do pracy w środowiskach zewnętrznych, w tym bateryjnych i niestabilnych komunikacyjnie.
## Wymagania funkcjonalne – jednostka główna (MCU)
1. Energooszczędny mikrokontroler 32-bitowy (np. RISC-V ESP32-C3 lub ARM Cortex-M4 STM32L476RG) z wystarczającą mocą do obsługi logiki systemowej, komunikacji i uruchamiania modeli TinyML / mikro-AI do autonomicznego podejmowania decyzji.
2. Obsługa wielu trybów oszczędzania energii (active/sleep/deep sleep/standby), z niskim poborem prądu i szybkim czasem wybudzania.
3. Wbudowany oscylator (RC/XTAL) zapewniający niezależność od zewnętrznych źródeł taktowania.
4. Kompatybilność z magistralami komunikacyjnymi: I²C, SPI, UART (obowiązkowe); PMBus i CAN (opcjonalne, w zależności od integracji z modułami).
5. Obsługa komunikacji z urządzeniami AT (np. modemy GSM/LTE) przez porty szeregowe.
6. Obsługa Wi-Fi (opcjonalna) – do komunikacji lokalnej lub konfiguracji.
7. Obsługa BLE (opcjonalna) – do komunikacji krótkiego zasięgu, konfiguracji lub diagnostyki.
8. Otwarte SDK i środowisko programistyczne (ESP-IDF, STM32 HAL, itp.), bez zamkniętych kompilatorów i toolchainów.
9. Dostępna i kompletna dokumentacja sprzętowa i software’owa.
10. Programowanie przez USB (opcjonalne) – preferowane w fazie testów lub aktualizacji polowej.
11. Wymagane wsparcie dla programowania przez UART, SWD/JTAG/ST-Link.
12. Możliwość aktualizacji OTA (opcjonalna) – najlepiej z podpisami cyfrowymi i zabezpieczeniami transmisji.
13. Wbudowany kontroler DMA – wymagany do efektywnej obsługi transmisji i akwizycji danych.
14. Sprzętowy RTC i watchdog (wewnętrzny lub zewnętrzny) – wymagane dla niezawodnej pracy systemu i zarządzania czasem.
15. Wsparcie dla stosu sieciowego i protokołów: HTTP, HTTPS, [[WebSocket]], [[MQTT]], [[JSON]], XML, z możliwością obsługi webhooków.




## Fallback i odporność systemu (rezyliencja)
1. Wsparcie dla niezależnych źródeł energii (np. zintegrowane moduły PV), z funkcją dynamicznego zarządzania poborem mocy – automatyczne odłączanie niewykorzystywanych modułów, zarządzanie zasilaniem per-segmentowym, i zaawansowane strategie oszczędzania energii (praca cykliczna, deep sleep, wake-on-event).
2. Redundancja zasilania poprzez możliwość równoległego wykorzystania wielu źródeł (zewnętrzne zasilacze DC, akumulatory, ogniwa PV), z zarządzaniem przez jeden lub więcej układów [[PMIC]]. System automatycznie przełącza się między źródłami, monitoruje parametry zasilania i zachowuje ciągłość pracy przy awarii dowolnego z nich.
3. Redundancja komunikacyjna oparta na równoległym wykorzystaniu wielu interfejsów transmisji danych (np. LTE/NB-IoT, GSM/SMS, LoRa/LoRaWAN, Wi-Fi, BLE). System posiada warstwę abstrakcji komunikacyjnej z logiką priorytetów, automatycznego przełączania i okresowego testowania łączności. Możliwość pracy w trybie degradacyjnym, z minimalną telemetrią przesyłaną kanałem awaryjnym.
4. Architektura modułowa systemu, umożliwiająca niezależną integrację, wymianę lub izolację poszczególnych komponentów (np. zasilania, komunikacji, czujników, pamięci). Każdy moduł posiada zdefiniowane interfejsy logiczne i fizyczne (np. UART/I²C/SPI, magistrale zasilania, złącza typu board-to-board).
5. System wyposażony w rezerwową jednostkę sterującą (backup MCU) z niezależnym zasilaniem i podstawową logiką awaryjną, działającą autonomicznie w przypadku całkowitej awarii głównego systemu. Backup MCU zapewnia m.in. transmisję sygnału awaryjnego, lokalizację, podstawową telemetrię oraz możliwość wymuszenia [[REST]]artu lub aktywacji podstawowych funkcji systemu.
6. Redundancja w warstwie zarządzającej: możliwość zdalnego lub automatycznego [[REST]]artu głównej jednostki logicznej (MCU/SoC) przez jednostkę pomocniczą lub watchdog sprzętowy. System wspiera fizyczne i programowe mechanizmy przejęcia kontroli przez jednostkę rezerwową oraz rekonfigurację po błędach krytycznych.
7. System zaprojektowany do samodzielnego przełączania się między trybami pracy i podejmowania decyzji w oparciu o lokalnie dostępne dane. W przypadku braku komunikacji z operatorem, logika awaryjna przejmuje kontrolę, umożliwiając kontynuowanie pracy w trybie „deep space probe” – z ograniczonym zestawem funkcji, autonomicznym raportowaniem i priorytetyzacją zadań.
8. Możliwość integracji szerokiej gamy czujników środowiskowych (m.in. akcelerometr, żyroskop, barometr, higrometr, termometr, czujnik światła, czujnik jakości powietrza), komunikujących się przez magistrale I²C, SPI lub UART. Dane z sensorów wykorzystywane są do oceny kontekstu operacyjnego, wykrywania anomalii, aktywacji trybów oszczędzania energii i wspomagania logiki autonomicznej.



## Pamięć i przechowywanie danych – wymagania techniczne
1. System powinien posiadać możliwość lokalnego zapisu danych telemetrycznych, logów, zrzutów awaryjnych oraz tymczasowych plików konfiguracji.
2. Obsługa wbudowanej pamięci Flash (min. 4 MB) lub zewnętrznej pamięci SPI Flash/FRAM do zapisu danych krytycznych i konfiguracji systemowej.
3. Opcjonalna obsługa kart microSD przez SPI lub SDIO, umożliwiająca logowanie danych z długiego okresu (np. sensory środowiskowe, ścieżki [[GNSS]], zdarzenia systemowe).
4. Wsparcie dla systemów plików typu LittleFS, SPIFFS lub FAT32, zależnie od nośnika i typu mikrokontrolera.
5. Możliwość cyklicznego nadpisywania, zarządzania przestrzenią i kontroli zużycia zapisu (wear leveling) — szczególnie dla pamięci typu Flash/SD.
6. Wymagana odporność danych na [[REST]]art systemu oraz zasilania (cache z synchronizacją, zapis atomowy, bezpieczne commit).
7. Pamięć może być używana również jako medium pośrednie dla przesyłania plików (eksport danych przez USB lub sieć).



## Sensory – wymagania techniczne
1. System powinien obsługiwać szeroką gamę czujników środowiskowych i ruchu, umożliwiających lokalne pozyskiwanie danych w celu wsparcia autonomicznych decyzji.
2. Obsługiwane klasy sensorów:
   - Ruchu: akcelerometr, żyroskop, magnetometr (IMU)
   - Atmosferyczne: barometr, higrometr, termometr
   - Środowiskowe: czujniki jakości powietrza (VOC, CO₂), światła, pyłów
   - Inne: czujniki dźwięku, zbliżeniowe, wilgotności gleby (jeśli wymagane przez przypadek użycia)
3. Komunikacja z sensorami przez magistrale I²C, SPI lub UART, z detekcją obecności i możliwością rekonfiguracji bez [[REST]]artu głównego systemu.
4. Obsługa dynamicznego odłączania/wybudzania sensorów w zależności od trybu pracy, poziomu energii i aktualnych potrzeb systemowych (power gating).
5. Dane z sensorów wykorzystywane do:
   - aktualizacji stanu operacyjnego systemu,
   - aktywacji/dezaktywacji trybów pracy,
   - wspomagania logiki autonomicznej i TinyML,
   - warunkowego wyzwalania zdarzeń lub alarmów.
6. Możliwość zapisu surowych danych w pamięci lokalnej i/lub ich strumieniowania przez kanały komunikacyjne ([[MQTT]]/HTTP/USB).
