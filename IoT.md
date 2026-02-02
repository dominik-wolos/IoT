# Internet Rzeczy (IoT) - Materiały do zaliczenia

## Spis treści
1. [Platformy sprzętowe](#platformy-sprzętowe)
2. [GPIO i piny](#gpio-i-piny)
3. [Interfejsy komunikacyjne](#interfejsy-komunikacyjne)
4. [Transmisja bezprzewodowa](#transmisja-bezprzewodowa)
5. [Protokoły sieciowe IoT](#protokoły-sieciowe-iot)
6. [Topologie sieci](#topologie-sieci)
7. [Sensory](#sensory)
8. [Środowiska programistyczne](#środowiska-programistyczne)
9. [Architektura mikrokontrolerów](#architektura-mikrokontrolerów)

---

## Platformy sprzętowe

### Raspberry Pi

#### Raspberry Pi 1 - Specyfikacja
- **SoC**: Broadcom BCM2835 (CPU + GPU + DSP + SDRAM w jednym)
- **CPU**: 700 MHz ARM1176JZF-S (ARM11 family)
- **GPU**: VideoCore IV - mikroprocesor wideo (H.264, OpenGL ES 2.0, 1080x1920 @ 60fps H.264 AVC)
- **Pamięć SDRAM**: 256 MB lub 512 MB (współdzielona z GPU)
- **Porty USB 2.0**: 1, 2 lub 4 (obsługiwane za pomocą zintegrowanego huba USB)
- **Storage**: karta microSD

#### Raspberry Pi 3 - Specyfikacja
- **Procesor**: Broadcom BCM2837, 64-bit, architektura ARMv8-A, **4 rdzenie 1.2 GHz**
- **Pamięć RAM**: 1 GB LPDDR2 900 MHz
- **Flash**: karta microSD
- **USB**: 4x USB 2.0 typ A
- **Wideo**: HDMI HD 1080 px / 30 fps, złącze kompozytowe (PAL, NTSC)
- **Audio**: 3.5 mm jack, HDMI
- **Połączenie z Internetem**:
  - Ethernet: 10/100 Mbps
  - Wi-Fi: 802.11 b/g/n, 50 Mbps
  - Bluetooth: BT 4.1
- **Zasilanie**: 5V 2.5A (poprzez złącze micro-USB)
- **Złącze rozszerzeń (GPIO)**: 40 pinów
- **Interfejs wyświetlacza**: DSI
- **Interfejs kamery**: CSI

---

### Arduino

#### Specyfikacja techniczna
- **Mikrokontrolery**: ATmega328, ATmega2560, ATmega32U4
- **Napięcie pracy**: zależy od typu (5V lub 3.3V)
- **Napięcie zasilania**: 7-12V
- **Porty**: USB typ B
- **Wyjścia cyfrowe I/O**: różne w zależności od modelu
- **Wyjścia cyfrowe obsługujące PWM**: zazwyczaj 6
- **Bootloader**: umożliwia programowanie przez USB bez dodatkowego programatora

#### Arduino - Proces kompilacji
1. Plik źródłowy (.ino)
2. Preprocesor (dodanie nagłówków, przetwarzanie dyrektyw)
3. Kompilator AVR-GCC
4. Linker
5. Plik HEX
6. Wgranie do mikrokontrolera

**Ważne**: Plik .ino jest automatycznie przekształcany przez Arduino IDE - dodawane są nagłówki i deklaracje funkcji.

---

### ESP8266

#### Charakterystyka
- Tani moduł Wi-Fi
- Bardzo popularny w projektach IoT
- Możliwość programowania jako samodzielny mikrokontroler
- **Napięcie pracy**: 3.3V
- **Wi-Fi**: 802.11 b/g/n
- **GPIO**: ograniczona liczba pinów

---

### ESP32

#### Specyfikacja techniczna
- **Procesor**: Dual-core (2 rdzenie)
- **Częstotliwość**: do 240 MHz
- **RAM**: 520 KB SRAM
- **Flash**: zewnętrzna pamięć flash
- **Komunikacja bezprzewodowa**:
  - Wi-Fi: 802.11 b/g/n
  - Bluetooth: BT 4.2 + BLE
- **GPIO**: 34 piny programowalne (nie wszystkie dostępne)
- **Interfejsy**:
  - 3x UART (RX/TX)
  - 2x SPI
  - 2x I2C
  - PWM na wszystkich pinach
  - ADC (18 kanałów)
  - DAC (2 kanały)
  - Sensor dotykowy (10 pinów)

#### ESP32 - Piny specjalne i ograniczenia

**Piny podłączone do pamięci FLASH** (nie używać):
- GPIO6, GPIO7, GPIO8, GPIO9, GPIO10, GPIO11

**UART - mapowanie pinów**:
| UART | RX | TX |
|------|----|----|
| UART0 | GPIO3 | GPIO1 |
| UART1 | GPIO9 | GPIO10 |
| UART2 | GPIO16 | GPIO17 |

**Uwagi**:
- **UART0**: odpowiada za komunikację ESP przez USB i procedury RESET/BOOT. Użycie ich zablokuje możliwość programowania układu.
- **UART1**: może być użyte do komunikacji, lecz w niektórych wersjach jest połączony z pamięcią FLASH.
- **UART2**: w pełni dostępne dla programisty.

**Strapping Pins** (wpływają na tryb rozruchu):
- GPIO0, GPIO2, GPIO5, GPIO12, GPIO15
- Te piny są odczytywane podczas startu ESP32 i decydują o trybie uruchomienia (BOOT/FLASH)

**Piny tylko INPUT**:
- GPIO34, GPIO35, GPIO36 (VP), GPIO39 (VN)
- Mogą być używane tylko jako wejścia (brak wewnętrznych pull-up/pull-down)

**Piny z ADC2** (konflikt z Wi-Fi):
- GPIO0, GPIO2, GPIO4, GPIO12, GPIO13, GPIO14, GPIO15, GPIO25, GPIO26, GPIO27
- Nie można używać ADC2, gdy Wi-Fi jest włączone

#### ESP32 - Zarządzanie energią

**Tryby niskiego poboru mocy**:
1. **Active Mode** - normalny tryb pracy
2. **Modem Sleep** - wyłącza Wi-Fi/Bluetooth, CPU działa
3. **Light Sleep** - zawiesza CPU, można wybudzić przez GPIO lub timer
4. **Deep Sleep** - tylko RTC działa, minimalne zużycie energii

**Sposoby wybudzania z Deep Sleep**:
- **Timer** - po określonym czasie
- **Touch pins** - przez piny dotykowe
- **ext0** - zewnętrzne wybudzenie przez jeden pin RTC_GPIO
- **ext1** - zewnętrzne wybudzenie przez wiele pinów RTC_GPIO

**Funkcje wybudzania**:
```c
esp_sleep_enable_timer_wakeup(time_in_us); // Timer
esp_sleep_enable_ext0_wakeup(gpio_num, level); // ext0
esp_sleep_enable_ext1_wakeup(mask, mode); // ext1
esp_sleep_enable_touchpad_wakeup(); // Touch
esp_deep_sleep_start(); // Wejście w Deep Sleep
```

---

## GPIO i piny

### Raspberry Pi - GPIO (General Purpose Input/Output)

#### Struktura pinów
- **40 pinów GPIO** (modele od Pi B+)
- Numeracja: piny fizyczne (1-40) vs. numery GPIO (BCM)

**Polecenie do wyświetlenia mapowania**:
```bash
gpio readall
```

#### Specjalne piny zasilania i masy
- **Piny 5V**: 2, 4
- **Piny 3.3V**: 1, 17
- **Piny GND (masa)**: 6, 9, 14, 20, 25, 30, 34, 39

#### Piny zarezerwowane
- **GPIO0 i GPIO1** (fizyczne piny 27 i 28) - zarezerwowane do użytku zaawansowanego (EEPROM I2C)

#### Napięcia logiczne
- **Wyjścia**: można ustawić na wysoki (3.3V) lub niski (0V)
- **Wejścia**: odczytywane jako wysoki (3.3V) lub niski (0V)
- **UWAGA**: Raspberry Pi **NIE** toleruje 5V na pinach GPIO! (może uszkodzić układ)

#### Interfejsy dostępne na GPIO

**PWM (Pulse Width Modulation)**:
- **Programowe PWM**: dostępne na wszystkich pinach (mniej precyzyjne)
- **Sprzętowe PWM**: tylko GPIO12, GPIO13, GPIO18, GPIO19

**SPI (Serial Peripheral Interface)**:
- **SPI0**: MOSI (GPIO10), MISO (GPIO9), SCLK (GPIO11), CE0 (GPIO8), CE1 (GPIO7)
- **SPI1**: MOSI (GPIO20), MISO (GPIO19), SCLK (GPIO21), CE0 (GPIO18), CE1 (GPIO17), CE2 (GPIO16)

**I2C (Inter-Integrated Circuit)**:
- **Dane**: GPIO2 (SDA)
- **Zegar**: GPIO3 (SCL)
- **EEPROM**: dane GPIO0, zegar GPIO1

**UART (Universal Asynchronous Receiver-Transmitter)**:
- **TX**: GPIO14
- **RX**: GPIO15

---

## Interfejsy komunikacyjne

### Podstawowe układy peryferyjne mikrokontrolerów

1. **Układy wejść-wyjść cyfrowych** - porty (ang. Ports)
2. **Układy czasowe** - timery/counters (ang. Timers/Counters Unit)
3. **Sterowniki komunikacji szeregowej** (ang. Serial Communication Unit)
4. **Układy specjalizowane**:
   - Przetworniki analogowo-cyfrowe (ADC)
   - Generatory PWM
   - Układy nadzorujące (Watchdog)

### Rozszerzanie liczby pinów I/O

Gdy liczba wyprowadzeń nie wystarcza:
1. Standardowe układy cyfrowe (CMOS, TTL)
2. Specjalizowane "układy rozszerzeń" łączone z szyną procesora
3. Układy łączone przez interfejs sterujący (I2C, SPI, 1-Wire)

---

### Transmisja danych

#### Rodzaje transmisji
1. **Transmisja równoległa**:
   - Jednoczesne przesyłanie wielu bitów
   - Wymaga wielu linii
   - Szybka, ale kosztowna (więcej przewodów)

2. **Transmisja szeregowa**:
   - Przesyłanie bit po bicie
   - Mniej linii
   - Wolniejsza, ale tańsza i lepsza na większe odległości

---

### UART (Universal Asynchronous Receiver-Transmitter)

#### Charakterystyka
- **Asynchroniczna** - brak sygnału zegarowego
- Dane przesyłane bajtami w postaci ciągów bitów
- Musi być ustalona częstotliwość przesyłania (baud rate)

#### Ramka danych UART
```
[Start bit][D0 D1 D2 D3 D4 D5 D6 D7][Parity][Stop bit]
```
- **Start bit**: 1 bit (informuje o początku transmisji)
- **Dane**: 5-9 bitów (najczęściej 8)
- **Parity bit**: opcjonalny (detekcja błędów)
- **Stop bit**: 1-2 bity (koniec transmisji)

#### Rodzaje transmisji
- **Simplex**: jednokierunkowa (tylko TX lub RX)
- **Half-duplex**: dwukierunkowa, ale nie jednocześnie
- **Full-duplex**: dwukierunkowa jednocześnie (dwie oddzielne linie: TX i RX)

#### Zalety i wady

**Zalety**:
- Połączenie dużej liczby układów peryferyjnych
- Niewielka liczba linii sterujących
- Mała liczba dodatkowych elementów
- Nie potrzebują miejsca w przestrzeni adresowej

**Wady**:
- Niezbędny specjalizowany hardware lub skomplikowane oprogramowanie
- Ograniczona prędkość transmisji

---

### SPI (Serial Peripheral Interface)

#### Charakterystyka
- **Synchroniczna** - z sygnałem zegarowym (SCLK)
- Model **Master-Slave**
- **Full-duplex** - jednoczesne wysyłanie i odbieranie

#### Linie SPI
- **MOSI** (Master Out Slave In) - dane z Mastera do Slave'a
- **MISO** (Master In Slave Out) - dane ze Slave'a do Mastera
- **SCLK** (Serial Clock) - sygnał zegarowy generowany przez Mastera
- **CS/SS** (Chip Select / Slave Select) - wybór urządzenia Slave (aktywny niski)

#### Zalety
- Wysoka prędkość transmisji (do kilkudziesięciu MHz)
- Full-duplex
- Prosty protokół
- Nie wymaga adresowania (CS wybiera urządzenie)

#### Wady
- Więcej linii niż I2C (4 + dodatkowe CS dla każdego urządzenia)
- Krótsze dystanse niż UART

---

### I2C (Inter-Integrated Circuit)

#### Charakterystyka
- **Synchroniczna** - z sygnałem zegarowym
- **Dwuprzewodowa**: SDA (dane) + SCL (zegar)
- Model **Multi-Master** - wiele urządzeń Master możliwych
- **Adresowanie** - każde urządzenie ma unikalny 7-bitowy lub 10-bitowy adres

#### Linie I2C
- **SDA** (Serial Data) - dwukierunkowa linia danych
- **SCL** (Serial Clock) - linia zegarowa

#### Zalety
- Tylko 2 linie (bez względu na liczbę urządzeń)
- Multi-Master
- Adresowanie urządzeń
- Stosunkowo prosta implementacja

#### Wady
- Wolniejsza niż SPI (do 400 kHz w trybie Fast Mode, 3.4 MHz w High Speed)
- Wymaga rezystorów podciągających (pull-up)
- Ograniczona liczba urządzeń (ze względu na adresy i pojemność linii)

---

### 1-Wire

#### Charakterystyka
- **Jednoprzewodowa** - dane + zasilanie na jednej linii
- Model **Master-Slave**
- Każde urządzenie ma unikalny 64-bitowy numer seryjny

#### Zalety
- Tylko 1 przewód + masa
- Możliwość zasilania pasożytniczego (urządzenia czerpią energię z linii danych)
- Automatyczna detekcja urządzeń

#### Wady
- Bardzo niska prędkość (15.4 kbps standardowo)
- Ograniczony zasięg

---

### CAN (Controller Area Network)

#### Charakterystyka
- Protokół używany w przemyśle i motoryzacji
- **Multi-Master**
- **Dwuprzewodowy**: CAN_H (High) i CAN_L (Low)
- Transmisja różnicowa (odporność na zakłócenia)
- Priorytetyzacja wiadomości

#### Zalety
- Bardzo odporny na zakłócenia
- Duże odległości (do 1 km przy niskich prędkościach)
- Priorytetyzacja
- Detekcja i korekcja błędów

#### Wady
- Skomplikowany protokół
- Wymaga kontrolera CAN
- Ograniczona długość wiadomości (8 bajtów danych)

---

## Modele komunikacji

### Master-Slave
- **Master** - urządzenie nadrzędne, inicjuje komunikację
- **Slave** - urządzenie podrzędne, odpowiada na polecenia
- Master odpytuje Slave'y o dane (polling)
- **Wady**: opóźnienia, uszkodzenie Mastera zatrzymuje system

### Multi-Master
- **Każdy węzeł może być Masterem**
- Węzeł wysyła wiadomość, gdy zachodzi potrzeba (bez czekania)
- Wymaga mechanizmu arbitrażu (kontrola dostępu do magistrali)
- **Zalety**: brak opóźnień, uszkodzenie jednego węzła nie zatrzymuje systemu

---

## Transmisja bezprzewodowa

### Bluetooth

#### Charakterystyka
- Standard komunikacji bezprzewodowej krótkiego zasięgu (10-100m)
- Pasmo: 2.4 GHz (ISM)
- **Bluetooth Classic**: dla przesyłania dźwięku, dużych danych
- **BLE (Bluetooth Low Energy)**: dla IoT, niskie zużycie energii

#### Wersje Bluetooth
- **BT 4.0, 4.1, 4.2**: wprowadzenie BLE
- **BT 5.0**: zwiększony zasięg (do 240m w otwartym terenie), większa prędkość
- **Prędkość**: do 2 Mbps (BT 5.0)

#### Zastosowania w IoT
- Smartwatche
- Czujniki zdrowia (pulsometry, glukometry)
- Urządzenia smart home
- Beacony

---

### Wi-Fi (802.11)

#### Charakterystyka
- Standard sieci bezprzewodowych
- Pasmo: 2.4 GHz (802.11b/g/n) i 5 GHz (802.11a/n/ac)
- Duże odległości (do kilkudziesięciu metrów w budynkach, ~300m na zewnątrz)

#### Standardy
- **802.11b**: do 11 Mbps (2.4 GHz)
- **802.11g**: do 54 Mbps (2.4 GHz)
- **802.11n**: do 600 Mbps (2.4 GHz i 5 GHz)
- **802.11ac**: do kilku Gbps (5 GHz)

#### Modulacje
- **DSSS** (Direct Sequence Spread Spectrum)
- **OFDM** (Orthogonal Frequency Division Multiplexing)
- **GFSK** (Gaussian Frequency Shift Keying)

---

### ZigBee

#### Charakterystyka
- Standard dla sieci bezprzewodowych krótkiego zasięgu
- Pasmo: 2.4 GHz (globalnie), 868 MHz (Europa), 915 MHz (USA)
- **Mesh networking** - możliwość tworzenia sieci kratowych
- Bardzo niskie zużycie energii

#### Zalety
- Niska cena
- Niskie zużycie energii
- Topologia mesh (sieć samoorganizująca się)
- Dobra penetracja budynków

#### Zastosowania
- Smart home (Philips Hue)
- Automatyka budynkowa
- Czujniki przemysłowe

---

### LoRaWAN (Long Range Wide Area Network)

#### Charakterystyka
- Technologia dalekiego zasięgu (do 15 km w mieście, do 50 km na wsi)
- Bardzo niskie zużycie energii
- Niska prędkość transmisji (250 bps - 50 kbps)
- Pasmo: sub-GHz (868 MHz w Europie, 915 MHz w USA)

#### Architektura
- **Węzły końcowe** (End Devices) - sensory, urządzenia
- **Bramy** (Gateways) - przekazują dane do serwera
- **Serwer sieciowy** (Network Server) - zarządza siecią
- **Serwer aplikacji** (Application Server) - przetwarza dane

#### Zastosowania
- Smart city
- Monitoring środowiska
- Rolnictwo precyzyjne
- Logistyka (tracking)

---

### Sieci komórkowe (Cellular)

#### Charakterystyka
- Wykorzystanie infrastruktury sieci komórkowych (2G, 3G, 4G LTE, 5G)
- Duży zasięg
- Wyższe koszty (abonament SIM)

#### Technologie dla IoT
- **NB-IoT** (Narrowband IoT):
  - Dla urządzeń stacjonarnych
  - Niskie zużycie energii
  - Dobra penetracja budynków

- **LTE-M** (LTE Cat-M1):
  - Dla urządzeń mobilnych
  - Wyższe prędkości niż NB-IoT
  - Obsługa połączeń głosowych

#### Zastosowania
- Liczniki smart metering
- Monitoring pojazdów (GPS tracking)
- Systemy alarmowe

---

### Z-Wave

#### Charakterystyka
- Standard dla smart home (1999)
- Pasmo: 868 MHz (Europa), 908 MHz (USA)
- Topologia mesh
- Zasięg: ~30m w budynkach

#### Zalety
- Dedykowany dla smart home
- Mniej zakłóceń niż 2.4 GHz
- Interoperacyjność urządzeń

#### Wady
- Zamknięty standard (wymaga licencji)
- Ograniczona liczba urządzeń w sieci (232)

---

### Thread

#### Charakterystyka
- Protokół dla smart home (opracowany przez Google, Apple)
- Pasmo: 2.4 GHz
- IPv6
- Mesh networking
- Niskie zużycie energii

#### Zalety
- Brak pojedynczego punktu awarii (mesh)
- Bezpieczeństwo (szyfrowanie)
- Integracja z Matter

---

### RFID (Radio-Frequency Identification)

#### Charakterystyka
- Technologia identyfikacji radiowej
- **Tag** (pasywny lub aktywny) + **Czytnik**

#### Częstotliwości
- **LF** (Low Frequency): 125-134 kHz - krótki zasięg (~10 cm)
- **HF** (High Frequency): 13.56 MHz - zasięg ~1m (NFC)
- **UHF** (Ultra High Frequency): 865-868 MHz (Europa), 902-928 MHz (USA) - zasięg do kilku metrów

#### Typy tagów
- **Pasywne**: bez baterii, zasilane przez pole elektromagnetyczne czytnika
- **Aktywne**: z baterią, większy zasięg

#### Zastosowania
- Kontrola dostępu
- Logistyka i magazynowanie
- Płatności zbliżeniowe (NFC)
- Identyfikacja zwierząt

---

## Protokoły sieciowe IoT

### MQTT (Message Queuing Telemetry Transport)

#### Charakterystyka
- Lekki protokół typu **publish-subscribe**
- Działa na TCP/IP
- Zaprojektowany dla urządzeń o ograniczonych zasobach

#### Architektura
- **Broker** - centralny serwer, zarządza komunikacją
- **Publisher** - publikuje wiadomości do tematów (topics)
- **Subscriber** - subskrybuje tematy i odbiera wiadomości

#### Quality of Service (QoS)
- **QoS 0**: At most once - bez potwierdzenia
- **QoS 1**: At least once - z potwierdzeniem (możliwe duplikaty)
- **QoS 2**: Exactly once - dokładnie raz (najbardziej niezawodne)

#### Zalety
- Niski narzut (małe nagłówki)
- Elastyczność (publish-subscribe)
- QoS - kontrola jakości dostarczenia

#### Zastosowania
- Smart home
- Monitoring przemysłowy
- Telemetria pojazdów

---

### XMPP (Extensible Messaging and Presence Protocol)

#### Charakterystyka
- Protokół bazujący na XML
- Komunikacja w czasie rzeczywistym
- Wcześniej znany jako Jabber

#### Zastosowania
- Czaty (np. Google Talk, WhatsApp w wczesnych wersjach)
- IoT (wymiana komunikatów i statusów)

---

### CoAP (Constrained Application Protocol)

#### Charakterystyka
- Protokół typu RESTful dla urządzeń o ograniczonych zasobach
- Działa na UDP (zamiast TCP jak HTTP)
- Podobny do HTTP, ale lżejszy

#### Metody CoAP
- GET, POST, PUT, DELETE (jak HTTP)

#### Zalety
- Mniejszy narzut niż HTTP
- Multicast
- Asynchroniczne wiadomości

---

### STOMP (Simple Text Oriented Messaging Protocol)

#### Charakterystyka
- Tekstowy protokół komunikacji z ramkami
- Oparty na HTTP
- Prosty w implementacji

---

## Topologie sieci

### 1. Magistrala (Bus)
- Wszystkie urządzenia podłączone do wspólnej linii
- **Zalety**: mało przewodów, łatwa rozbudowa
- **Wady**: kolizje, awaria magistrali = awaria sieci

### 2. Gwiazda (Star)
- Centralne urządzenie (hub/switch), do którego podłączone są wszystkie węzły
- **Zalety**: brak kolizji, łatwa diagnostyka
- **Wady**: awaria centrum = awaria sieci, więcej przewodów

### 3. Pierścień (Ring)
- Urządzenia połączone w zamknięty pierścień
- **Zalety**: deterministyczny czas transmisji
- **Wady**: awaria jednego węzła może zatrzymać sieć

### 4. Siatka (Mesh)
- Każdy węzeł połączony z wieloma innymi
- **Zalety**: duża niezawodność, redundancja
- **Wady**: skomplikowana, droższa

### 5. Drzewo (Tree)
- Hierarchiczna struktura (połączenie gwiazdy i magistrali)
- **Zalety**: skalowalność, podział na segmenty
- **Wady**: awaria węzła nadrzędnego = awaria poddrzewa

---

## Sensory

### Klasyfikacja sensorów

#### Ze względu na sposób detekcji
1. **Elektryczne** - pomiar wielkości elektrycznych (napięcie, prąd, opór)
2. **Optyczne** - detekcja światła, podczerwieni
3. **Mechaniczne** - pomiar siły, ciśnienia, przyspieszenia
4. **Chemiczne** - detekcja gazów, pH, wilgotności
5. **Termiczne** - pomiar temperatury

#### Ze względu na sygnał wyjściowy
1. **Analogowe** - ciągły sygnał (napięcie, prąd)
2. **Cyfrowe** - sygnał dyskretny (I2C, SPI, 1-Wire)

---

### Sensory ruchu i pozycji

#### Akcelerometry
- **Pomiar**: przyspieszenie liniowe (w osiach X, Y, Z)
- **Jednostka**: g (1g = 9.81 m/s²)
- **Typ**: MEMS (mikroelektromechaniczny)
- **Zastosowania**:
  - Detekcja orientacji (poziom, pochylenie)
  - Wykrywanie wstrząsów, wibracji
  - Krokomierze
  - Kontrolery gier

#### Żyroskopy
- **Pomiar**: prędkość kątowa (obrotu)
- **Jednostka**: °/s (stopnie na sekundę)
- **Typ**: MEMS
- **Zastosowania**:
  - Stabilizacja obrazu (kamery)
  - Nawigacja (drones, roboty)
  - Gry (kontrolery ruchu)

#### Magnetometry
- **Pomiar**: pole magnetyczne (kompas elektroniczny)
- **Jednostka**: μT (mikrotesla) lub Gauss
- **Zastosowania**:
  - Kompas cyfrowy
  - Detekcja metali
  - Nawigacja

#### IMU (Inertial Measurement Unit)
- Połączenie: akcelerometr + żyroskop + (opcjonalnie) magnetometr
- **Przykład**: MPU6050 (6-DOF: 3-axis accel + 3-axis gyro)

---

### Sensory środowiskowe

#### Temperatura
- **Typy**:
  - **Termistory** (NTC, PTC) - zmiana rezystancji z temperaturą
  - **Termotranzystory** - pomiar w półprzewodniku
  - **Cyfrowe** (DS18B20, DHT22) - wyjście cyfrowe
- **Zastosowania**: stacje pogodowe, termostat, monitoring

#### Wilgotność
- **Typy**:
  - **Pojemnościowe** - zmiana pojemności z wilgotnością
  - **Rezystancyjne** - zmiana rezystancji
- **Często w połączeniu z sensorem temperatury** (np. DHT22, BME280)

#### Ciśnienie
- **Typy**:
  - **Piezorezystancyjne** (MEMS)
  - **Pojemnościowe**
- **Przykłady**: BMP280, BMP180
- **Zastosowania**: altimetry, prognoza pogody

#### Jakość powietrza
- **Sensory gazów**:
  - **MQ-2**: dym, LPG, metan
  - **MQ-135**: CO2, NH3, benzen
  - **MQ-7**: tlenek węgla (CO)
- **Sensory PM** (particulate matter):
  - **PMS5003**: pomiar pyłów zawieszonych (PM2.5, PM10)

---

### Sensory światła

#### Fotorezystory (LDR)
- Zmiana rezystancji w zależności od natężenia światła
- Prosty, tani
- **Zastosowania**: detekcja zmierzchu, automatyczne oświetlenie

#### Fotodiody
- Generują prąd proporcjonalny do natężenia światła
- Szybsze niż fotorezystory

#### Sensory UV
- Pomiar promieniowania ultrafioletowego
- **Przykład**: VEML6070

#### Sensory koloru
- Pomiar intensywności światła w różnych długościach fal (RGB)
- **Przykład**: TCS3200

---

### Sensory odległości

#### Ultrasoniczne (HC-SR04)
- **Zasada**: wysyłanie ultradźwięków, pomiar czasu odbicia
- **Zasięg**: 2 cm - 4 m
- **Dokładność**: ~3 mm
- **Zastosowania**: roboty autonomiczne, parktronic

#### Podczerwień (IR)
- **Sharp GP2Y0A21YK0F**: zasięg 10-80 cm
- **Zasada**: pomiar intensywności odbitego światła IR

#### Laserowe (LiDAR)
- **Time-of-Flight (ToF)**
- Bardzo precyzyjne, długi zasięg
- **Przykład**: VL53L0X (do 2m)

---

### Sensory detekcji

#### PIR (Passive Infrared)
- **Detekcja**: ruchu przez zmianę promieniowania podczerwonego
- **Zastosowania**: alarmy, automatyczne oświetlenie

#### Hallotron (Hall Effect Sensor)
- **Detekcja**: pola magnetycznego
- **Zastosowania**: liczniki obrotów, detekcja zamknięcia drzwi/okien

---

### Sensory elektrochemiczne

#### Sensory pH
- Pomiar kwasowości/zasadowości roztworu
- **Zakres**: 0-14 pH

#### Sensory tlenu
- Pomiar stężenia O2 w gazie lub ciecz

#### Sensory wilgotności gleby
- Pomiar wilgotności ziemi (dla rolnictwa, ogrodnictwa)

---

## Środowiska programistyczne

### Arduino IDE

#### Charakterystyka
- Podstawowe środowisko dla Arduino
- Język: C/C++ z uproszczeniami
- **Struktura programu**:
  ```cpp
  void setup() {
    // Kod inicjalizujący (wykonuje się raz)
  }

  void loop() {
    // Kod główny (wykonuje się w pętli)
  }
  ```

#### Proces kompilacji
1. Kod źródłowy (.ino)
2. Preprocessing (dodanie Arduino.h, deklaracji funkcji)
3. Kompilacja (avr-gcc / xtensa-gcc)
4. Linkowanie bibliotek
5. Plik HEX
6. Upload do mikrokontrolera

#### Bootloader
- Program w pamięci flash mikrokontrolera
- Umożliwia wgrywanie kodu przez UART (USB)
- Sprawdza przy starcie, czy jest próba wgrania nowego kodu
- Dla Arduino: **Optiboot** (optymalizowana wersja)

**Lokalizacja bootloadera**:
```
<Arduino_folder>/hardware/arduino/avr/bootloaders/optiboot/
```

---

### Inne środowiska dla Arduino

1. **PlatformIO** (dodatek do VS Code):
   - Wsparcie dla wielu platform
   - Zarządzanie bibliotekami
   - Zaawansowane debugowanie

2. **Visual Micro** (dodatek do Visual Studio):
   - Integracja z Visual Studio
   - IntelliSense
   - Debugowanie

3. **Arduino Eclipse** (dodatek do Eclipse):
   - Zaawansowane narzędzia
   - Debugowanie

4. **embedXcode** (dla Xcode na macOS):
   - Dedykowany dla użytkowników macOS

---

### Języki programowania dla IoT

#### C/C++
- **Dla**: Arduino, ESP32, ESP8266, STM32
- **Zalety**: szybkość, kontrola sprzętu, mało pamięci
- **Wady**: trudniejszy, wymaga kompilacji

#### Python
- **Dla**: Raspberry Pi
- **Zalety**: łatwość, duża liczba bibliotek
- **Wady**: wolniejszy, więcej pamięci

#### MicroPython
- **Dla**: ESP32, ESP8266, Pyboard
- **Zalety**: Python na mikrokontrolerach
- **Wady**: ograniczone możliwości, wolniejszy niż C

#### Lua
- **Dla**: ESP8266 (NodeMCU)
- **Zalety**: prosty, skryptowy
- **Wady**: ograniczone wsparcie

---

## Architektura mikrokontrolerów

### Rodzaje rdzeni ARM

#### ARM Cortex-M (dla mikrokontrolerów)
- **Cortex-M0/M0+**: najprostsze, 32-bit, niskie zużycie energii
- **Cortex-M3**: pipeline 3-stopniowy, MPU
- **Cortex-M4**: jak M3 + DSP + FPU (opcjonalnie)
- **Cortex-M7**: najwydajniejszy, cache, FPU

#### ARM Cortex-A (dla aplikacji, SBC)
- **ARMv8** (64-bit): Raspberry Pi 3, 4
- **ARMv7** (32-bit): starsze Pi

#### Charakterystyka ARM
- **RISC** (Reduced Instruction Set Computer)
- **Pipeline**: wykonywanie wielu instrukcji jednocześnie
- **Thumb**: zestaw instrukcji 16-bitowych (oszczędność pamięci)

---

### SoC (System on Chip)

#### Definicja
- Kompletny system komputerowy na jednym układzie
- Zawiera: CPU, GPU, RAM, kontrolery I/O, moduły RF

#### Przykłady
- **Broadcom BCM2837** (Raspberry Pi 3): CPU + GPU + RAM
- **ESP32**: CPU + Wi-Fi + Bluetooth + RAM

---

### SBC (Single-Board Computer)

#### Definicja
- Kompletny komputer na jednej płytce drukowanej
- Zawiera: mikroprocesor/SoC, pamięć, I/O, zasilanie

#### Przykłady
- **Raspberry Pi**: najpopularniejszy SBC
- **Orange Pi**
- **BeagleBone**

---

## Rozruch mikrokontrolera

### Proces startowy
1. **Reset** - wektor resetu (adres pierwszej instrukcji)
2. **Bootloader** (opcjonalnie):
   - Sprawdza, czy jest próba wgrania nowego programu
   - Jeśli tak: odbiera dane przez UART i zapisuje do flash
   - Jeśli nie: przeskakuje do programu użytkownika
3. **Program użytkownika**:
   - Inicjalizacja (setup)
   - Pętla główna (loop)

### ESP32 - Rozruch
1. **ROM Bootloader** (First Stage Bootloader):
   - Wbudowany w ROM (niemodyfikowalny)
   - Sprawdza strapping pins (GPIO0, GPIO2...)
   - Decyduje o trybie: Flash Boot / UART Download
2. **Second Stage Bootloader** (w flash):
   - Inicjalizuje pamięć flash
   - Ładuje partycje
3. **Program aplikacji**

---

## Dobre praktyki w IoT

### Bezpieczeństwo
1. **Szyfrowanie komunikacji**: TLS/SSL dla MQTT, HTTPS
2. **Autentykacja**: tokeny, certyfikaty
3. **Aktualizacje OTA** (Over-The-Air): zdalne aktualizacje firmware
4. **Minimalizacja uprawnień**: tylko niezbędne funkcje

### Zarządzanie energią
1. **Deep Sleep**: dla urządzeń bateryjnych
2. **Optymalizacja częstotliwości**: CPU, Wi-Fi tylko gdy potrzeba
3. **Wake-up triggers**: wybudzanie tylko gdy potrzeba (timer, GPIO)

### Niezawodność
1. **Watchdog**: automatyczny reset przy zawieszeniu
2. **Retry logic**: ponawianie połączeń
3. **Error handling**: obsługa błędów transmisji

---

## Pytania egzaminacyjne - przygotowanie

### Platformy sprzętowe
1. Jakie są różnice między Raspberry Pi a Arduino?
2. Wymień specyfikację ESP32 (CPU, RAM, interfejsy).
3. Które piny ESP32 są podłączone do pamięci FLASH?
4. Co to są strapping pins w ESP32?
5. Jakie tryby zarządzania energią ma ESP32?

### GPIO
1. Ile pinów GPIO ma Raspberry Pi 3?
2. Które piny Raspberry Pi są zasilane 5V, a które 3.3V?
3. Wymień interfejsy dostępne na GPIO Raspberry Pi (SPI, I2C, UART, PWM).
4. Czym różni się programowe PWM od sprzętowego?

### Interfejsy
1. Czym różni się UART od USART?
2. Opisz ramkę danych UART.
3. Jakie są różnice między SPI a I2C?
4. Wymień linie SPI i ich funkcje.
5. Czym jest adresowanie w I2C?
6. Jakie są zalety i wady interfejsu 1-Wire?
7. Opisz protokół CAN i jego zastosowania.

### Transmisja bezprzewodowa
1. Jakie są różnice między Bluetooth Classic a BLE?
2. Wymień standardy Wi-Fi i ich prędkości.
3. Czym różni się ZigBee od Wi-Fi?
4. Do czego służy LoRaWAN i jaki ma zasięg?
5. Czym różni się NB-IoT od LTE-M?
6. Jakie częstotliwości używa RFID (LF, HF, UHF)?

### Protokoły IoT
1. Opisz model publish-subscribe w MQTT.
2. Jakie są poziomy QoS w MQTT?
3. Czym różni się MQTT od HTTP?
4. Do czego służy protokół CoAP?

### Sensory
1. Co mierzy akcelerometr, a co żyroskop?
2. Jak działa czujnik ultradźwiękowy HC-SR04?
3. Wymień sensory jakości powietrza (gazy, PM).
4. Czym różni się fotorezystor od fotodiody?
5. Do czego służy czujnik PIR?

### Programowanie
1. Opisz strukturę programu Arduino (setup, loop).
2. Co to jest bootloader i do czego służy?
3. Jakie są różnice między programowaniem w C a Python dla IoT?
4. Jak wygląda proces kompilacji kodu Arduino?

### Architektura
1. Czym różni się SoC od SBC?
2. Wymień rodzaje rdzeni ARM Cortex-M.
3. Opisz proces rozruchu mikrokontrolera.
4. Co to jest watchdog timer?

---

## Źródła i materiały dodatkowe

- Dokumentacja Raspberry Pi: https://www.raspberrypi.org/documentation/
- Dokumentacja Arduino: https://www.arduino.cc/reference/
- ESP32 Technical Reference: https://www.espressif.com/
- MQTT.org: https://mqtt.org/
- Specyfikacje protokołów: IEEE, IETF

---

**Powodzenia na zaliczeniu!**
