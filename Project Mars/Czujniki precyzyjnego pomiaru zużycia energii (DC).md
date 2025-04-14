# Czujniki precyzyjnego pomiaru zużycia energii (DC)

Czujniki podobne do rodziny **INAxxx** do zastosowań telemetrycznych (np. ESP32 + LoRa) o **niskim zużyciu mocy** i **wysokiej dokładności pomiaru**.

---

## ⚙️ Kluczowe czujniki

| Model        | Typ pomiaru             | Zakres napięcia / prądu       | Interfejs | Rozdzielczość | Uwagi techniczne                                          |
|--------------|--------------------------|-------------------------------|-----------|----------------|-----------------------------------------------------------|
| **INA219**   | napięcie + prąd + moc    | 0–26V / ±3.2A (zależnie od Rshunt) | I²C       | 12–15 bitów     | Tani, popularny, dobre wsparcie softu                     |
| **INA226**   | napięcie + prąd + moc    | do 36V / zależnie od shunta  | I²C       | 16 bitów        | Programowalna rozdzielczość, **bardzo dobry wybór**       |
| **INA260**   | napięcie + prąd + moc    | do 36V / **wbudowany shunt 15 mΩ** | I²C       | 16 bitów        | Bardzo wygodny – brak zewnętrznego shunta                 |
| **INA238**   | napięcie + prąd + moc    | do 85V / ±10–12.5A            | I²C       | 16+ bitów       | **Nowoczesny, bardzo precyzyjny**, niski offset, szybki ADC |
| **INA3221**  | 3 kanały (multi-rail)    | do 26V                        | I²C       | 12–16 bitów     | Pomiar 3 niezależnych źródeł (np. 3,3V / 5V / VBAT)       |

---

## ✅ Dobór czujnika wg zastosowania

| Zastosowanie                           | Czujnik                      | Uzasadnienie techniczne                                |
|----------------------------------------|------------------------------|---------------------------------------------------------|
| Pomiar energii układu ESP / LoRa       | **INA226** lub **INA260**    | Balans: dokładność, prostota, niska cena                |
| Pomiar bardzo małych prądów (µA–mA)    | **INA238**                   | Bardzo niski offset, szybki ADC, duży zakres dynamiczny |
| Pomiar wielu napięć jednocześnie       | **INA3221**                  | Jeden układ, 3 niezależne wejścia                       |
| Minimum zewnętrznych elementów         | **INA260**                   | Ma wszystko – 1 chip, łatwe podłączenie                 |

---

## 🔋 Zużycie energii – dokładny pomiar

1. **INA226/INA238** umożliwiają precyzyjne próbkowanie napięcia/prądu i przeliczanie na energię (Wh).
2. Integracja z **RTC** lub timerem → liczenie zużycia energii w czasie.
3. Do pomiarów < 1 µA warto rozważyć wzmacniacze operacyjne typu *zero-drift* + ADC o dużej rozdzielczości.

---

## 🛒 Ceny (orientacyjnie)

| Model     | Cena modułu | Uwagi                                |
|-----------|-------------|--------------------------------------|
| INA219    | ~1–2 USD    | Słabszy od INA226, ale tani          |
| INA226    | ~2–3 USD    | Najlepszy stosunek cena/jakość       |
| INA260    | ~3–5 USD    | Wygoda – brak shunta                 |
| INA238    | ~4–6 USD    | Nowość, jeszcze nie wszędzie dostępna|

---

## 📦 Kod i dalsze kroki

