# Artemis – główna jednostka decyzyjna systemu M.A.R.S.

## Filozofia

Artemis to serce systemu M.A.R.S. – jego inteligencja, logika i strategia. To jednostka odpowiedzialna za **podejmowanie decyzji operacyjnych w czasie rzeczywistym**, przetwarzanie danych z sensorów, koordynację modułów komunikacyjnych oraz planowanie cykli energetycznych. Artemis ma zdolność samodzielnego podejmowania decyzji opartych na danych, wspierając się lokalnymi modelami TinyML oraz logiką stanu. To ona prowadzi M.A.R.S., dopóki działa choć jeden moduł.

---

## Zadania Artemis

1. **Zbieranie i przetwarzanie danych z czujników** (I²C/SPI/ADC/RTC)
2. **Lokalna analiza i klasyfikacja danych** – wsparcie TinyML
3. **Zarządzanie stanami zasilania, trybami pracy i cyklami aktywności systemu**
4. **Obsługa logiki decyzyjnej i reagowanie na zdarzenia (timery, czujniki, watchdogi)**
5. **Nadzór nad komunikacją z systemami zewnętrznymi** (MQTT/HTTP/SMS)
6. **Współpraca i synchronizacja z Atheną (rezerwowe MCU)**
7. **Logowanie, synchronizacja i transfer danych telemetrycznych**

---

## Wybrany mikrokontroler: **SparkFun Artemis (Apollo3 Blue)**

### Główne cechy:

- 32-bitowy ARM Cortex-M4F, do 96 MHz (turboSPOT®)
- FPU, DMA, MPU, RTC, cache
- 1 MB Flash, 384 KB RAM
- Bluetooth Low Energy 5
- Zasilanie 1.755–3.63 V, Deep Sleep: ~1 µA
- PDM, I²S, 14-bit ADC, 15 kanałów
- 6x I²C/SPI master, 2x UART, 1x slave SPI/I²C
- 50 GPIO, PWM, timery, temp sensor, watchdog
- RTC + XTAL 32.768 kHz, precyzyjny oscylator
- Obsługa zewnętrznej pamięci (MSPI, QSPI)

---

## Interfejsy komunikacyjne

- **UART x2** – komunikacja z modemem GSM, GNSS, konsola debug
- **I²C/SPI x6** – czujniki, PMIC, współpraca z Atheną, pamięci zewnętrzne
- **MSPI/QSPI x1** – szybka pamięć zewnętrzna / zasoby kodu
- **ADC 14-bit, 15 kanałów** – pomiar napięcia, stanu baterii, sensory analogowe
- **PDM/I²S** – obsługa mikrofonów/akcelerometrów audio
- **GPIO/PWM** – kontrola linii, sygnalizacja, zasilanie, przekaźniki

---

## Interakcje z Atheną

- Wysyłanie heartbeat/logów (UART/I²C)
- Przekazywanie stanu i rozkazów zarządzania energią
- Umożliwienie przejęcia kontroli przez Athenę (zapis danych, standby)
- Obsługa mechanizmów resetu lub reprogramowania przez Athenę

---

## Interakcje z systemem

- Odczyt danych z czujników i ich wstępna analiza
- Komunikacja przez BLE, UART, SPI, MQTT/HTTP (przez inne moduły)
- Współpraca z PMIC w zakresie zarządzania zasilaniem
- Obsługa logiki trybu misji: pełna aktywność ↔ degradacja ↔ czuwanie

---

## Tryby operacyjne Artemis

1. **Tryb nominalny** – pełna aktywność, analiza, komunikacja, rejestracja danych
2. **Tryb oszczędny** – tylko istotne sensory i komunikacja z wybranymi interwałami
3. **Tryb diagnostyczny** – aktywna wymiana z Atheną, kontrola integralności
4. **Tryb uśpienia** – DeepSleep z RTC, wybudzanie przez zdarzenia zewnętrzne
5. **Tryb przejęcia przez Athenę** – pełna pasywność, oczekiwanie na reset/recovery

---

## Status

- SparkFun Artemis z procesorem Apollo3 Blue wybrany jako jednostka nadrzędna systemu M.A.R.S.
- W pełni zgodny z założeniami energetycznymi, komunikacyjnymi i logicznymi
- Gotowy do integracji z TinyML, PMIC, RTC, sensorami i układami komunikacyjnymi
