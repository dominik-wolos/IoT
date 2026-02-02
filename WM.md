# Grafika 3D, VR/AR/MR i Druk 3D - Notatki do egzaminu

## 1. VR - Virtual Reality (Wirtualna Rzeczywistość)

### Definicja
- Sposób wykorzystania technologii komputerowej w tworzeniu interaktywnego, trójwymiarowego świata
- Obiekty 3D/2D sprawiają wrażenie przestrzennej obecności
- Wymaga wygenerowania osobnych obrazów na lewe i prawe oko

### Kluczowe pojęcia
- **Immersja** - proces zanurzenia się w świat wirtualny, złudzenie otoczenia przez obiekty graficzne
  - Może wywoływać: mdłości, zawroty głowy, utratę równowagi, bóle głowy
- **Interakcja** - możliwość oddziaływania na wirtualne obiekty podczas przemieszczania się
  - Kontrolery trzymane w rękach
  - Dłuższe wpatrywanie się w obiekty
  - Podświetlenia, klikanie przycisków, wyświetlanie informacji

### Zestaw Omni
- Bieżnia omni-track - naturalne poruszanie się w VR
- Czujniki ruchu ciała
- Buty Omni - odpowiedni poślizg
- Pasy Omni - stabilizacja i pozycjonowanie
- Gogle HTC Vive
- Kontrolery HTC
- Optymalna wartość: **90 FPS** (minimalizuje chorobę lokomocyjną)

### Niskokosztowy zestaw VR
- Aparat standardowy
- Laptop
- Bezpłatne oprogramowanie (3ds Max, Gimp, Unity 3D)
- Gogle Samsung Gear VR + smartfon

---

## 2. AR - Augmented Reality (Rozszerzona Rzeczywistość)

### Definicja
- System łączący świat rzeczywisty ze światem generowanym komputerowo
- Na obraz z kamery nałożona jest grafika 2D/3D generowana w czasie rzeczywistym
- Użytkownik może obserwować rzeczywistość z nałożonymi elementami wirtualnymi

### Zastosowanie
- Półprzezroczyste okulary
- Kody QR do generowania obiektów wirtualnych
- Nakładanie informacji na rzeczywisty obraz

---

## 3. MR - Mixed Reality (Rzeczywistość Mieszana)

### Definicja
- Wtapianie elementów rzeczywistych w wirtualne środowisko i odwrotnie
- Umieszczanie modeli 3D i obiektów 2D w przestrzeni rzeczywistej

### Technologia
- Okulary MR z kamerami głębokości mapującymi przestrzeń
- Wirtualna siatka nakładana na obiekty
- Uwzględnia:
  - **Z-index** - pomiar odległości obiektów od kamery
  - **Okluzja** - wzajemne przesłanianie się obrazów

---

## 4. Druk 3D (Rapid Prototyping)

### Definicja
- Zestaw technik tworzenia obiektów fizycznych na podstawie modeli cyfrowych
- Technika naddatkowa - dodawanie kolejnych warstw
- Grubość warstwy: **0,01 do 0,2 mm**

### Główne technologie

#### FDM/FFF (Fused Deposition Modelling)
- Drukowanie z tworzyw termoplastycznych
- Wytłaczanie stopionego materiału przez podgrzewaną głowicę
- Uniwersalna - może użyć plastiku, betonu, gliny, żywych tkanek, czekolady

#### SLS (Selective Laser Sintering)
- Spiekanie kolejnych warstw proszków polimerowych
- Utwardzanie wiązką lasera

#### SLA (Stereolitografia)
- Fotoutwardzanie materiału (wiązka UV z laserem)
- Duża dokładność wymiarowa
- Połowa lat 80-tych (Chuck Hull)

#### SLM (Selective Laser Melting)
- Selektywne stapianie materiału (proszki brązu, stali, tytanu)
- Laser dużej mocy

#### 3D Printing
- Natryskowe spajanie materiału proszkowego
- Możliwość drukowania kolorowego (CMYK)

### Proces drukowania 3D
1. **Modelowanie 3D** - warunek wodoszczelności
2. **Drukowanie** - generowanie g-codu, slicery (KISSlicer, Cura, MatterControl)
3. **Wykończenie** - usuwanie podpór

### Wnętrze modelu
- Struktura wypełniająca (wybór kształtu i gęstości)
- Wpływ na sztywność, ilość materiału, czas druku (20-30 godz. dla obiektów ~20 cm)

---

## 5. Grafika Komputerowa - Podstawy

### Grafika Bitmapowa (Rastrowa)
**Charakterystyka:**
- Piksel = najmniejszy element obrazu
- Zapis współrzędnych piksela i jego barwy
- Cały obraz = jeden obiekt
- Doskonale odzwierciedla nieregularne kształty
- Częściowo skalowalna

**Zastosowanie:**
- Zdjęcia cyfrowe
- Wypełnienia obiektów wektorowych
- Tekstury dla obiektów 3D
- Tło w grafice 2D i 3D

**Formaty:**
- Z kompresją bezstratną: .tiff, .png, .gif, .bmp
- Z kompresją stratną: .jpg, .jps, .jpg2000
- Bez kompresji: .psd, .xcf

### Grafika Wektorowa
**Charakterystyka:**
- Zapis przez równania matematyczne (geometria analityczna)
- Każdy element = osobny obiekt
- Pełna skalowalność
- Nadaje się do kształtów regularnych

### Grafika Fraktalna
**Charakterystyka:**
- Zapisana przez formuły rekurencyjne
- Cecha samopodobieństwa
- Wymiar rzeczywisty (nie naturalny), np. 2,34
- Można przybliżać w nieskończoność
- 1982 - Benoit Mandelbrot "The fractal geometry of nature"

---

## 6. Modelowanie 3D

### Typy modelowania
- **Parametryczne** - równania matematyczne (geometria wykreślna)
- **Siatkowe** - siatka trójkątów i czworokątów

### Elementy siatki (mesh)
- **Vertices** - wierzchołki
- **Edges** - krawędzie
- **Faces** - trójkąty
- **Polygons** - prostokątne elementy
- **Surfaces** - powierzchnie

### Techniki modelowania

#### 1. Modelowanie na podstawie profili 2D
- **Extrude** - wytłaczanie wzdłuż wektora
- **Sweep** - wytłaczanie po ścieżce
- **Loft** - łączenie przekrojów
- **Lathe** - obrót wokół osi

#### 2. Constructive Solid Geometry (CSG)
Operacje Boole'a:
- **Union** - dodawanie (A+B, usuwa część wspólną)
- **Subtraction A-B** - odejmowanie
- **Subtraction B-A** - odejmowanie odwrotne
- **Intersection** - część wspólna

#### 3. Subdivision Surfaces
- Utworzenie prostej bryły i dzielenie jej
- Formowanie pożądanego kształtu

#### 4. Edycja obiektów - Modyfikatory
- **Bend** - zginanie względem osi
- **Twist** - skręcanie wokół osi
- **Taper** - przewężenie
- **Stretch** - ściskanie/rozciąganie

#### 5. Edycja siatki
Narzędzia:
- **Extrude** - tworzy nową płaszczyznę
- **Bevel** - tworzy nową płaszczyznę i zmienia rozmiar
- **Bridge** - łączy zaznaczenia
- **Outline** - powiększa/pomniejsza
- **Inset** - tworzy mniejszą płaszczyznę na zaznaczonej
- **Chamfer** - tworzy fazę lub zaokrąglenie
- **Flip** - odwraca wektor

### Mapowanie (Teksturowanie)
- Odwzorowanie współrzędnych 2D tekstury na współrzędne 3D
- **UVW Map** - wybór typu mapowania (płaskie, sferyczne, cylindryczne, sześcienne)
- **Unwrap UVW** - bardziej zaawansowane, edycja każdego punktu mapy

---

## 7. Skanowanie 3D

### Typy skanerów
- **Kontaktowe** - fizyczny dotyk
- **Bezkontaktowe aktywne** - emitują promieniowanie (światło, ultradźwięki, rtg)
- **Bezkontaktowe pasywne** - detekcja odbitego światła otoczenia

### Skaner na światło strukturalne
- Projekcja wzorów świetlnych na obiekt
- Analiza deformacji wzorów
- Skanowanie całego obszaru jednocześnie
- Rejestracja tekstury

### Parametry skanerów (przykład Artec)

| Parametr | Artec Eva | Artec Spider |
|----------|-----------|--------------|
| Rozdzielczość 3D | 0,5 mm | 0,1 mm |
| Dokładność punktu | 0,1 mm | 0,05 mm |
| Pole widzenia | 214×148 mm do 536×371 mm | 90×70 mm do 180×140 mm |
| Odległość od obiektu | 0,4-1 m | 0,17-0,35 m |
| FPS | 16 fps | 7,5 fps |
| Technologia | Światło białe | Światło niebieskie |

### Przygotowanie obiektu

**Powierzchnie trudnoskanowalne:**
- Czarne/bardzo ciemne → Spray antyrefleksyjny
- Błyszczące → Spray antyrefleksyjny, przechył skanera
- Przezroczyste (szkło) → Spray antyrefleksyjny
- Cienkie krawędzie → Dodaj geometrię tła

### Algorytm skanowania
1. Uruchomienie programu (np. Artec Studio)
2. Podgląd (F7)
3. Nagrywanie
4. Obróć obiekt, skanuj pozostałe strony

### Podstawowe zasady
1. Uwaga na obiekt na ekranie, nie rzeczywisty
2. Nie poruszaj skanera zbyt szybko
3. Trzymaj obiekt w centrum pola widzenia
4. Optymalna wartość: środek miernika zasięgu
5. Zapewnij wspólne obszary między skanami
6. Nie rejestruj zbyt wielu klatek

---

## 8. Obróbka Chmury Punktów

### Środowisko pracy
- Pasek narzędzi (Tools)
- Obszar roboczy (Workspace)
- Panel Workspace - lista skanów
- Okno z logami

### Ogólna procedura
1. **Czyszczenie skanów** - usunięcie niepożądanych elementów
2. **Dopasowanie skanów** - uzyskanie kompletnej bryły
3. **Rejestracja** - optymalizacja pozycji klatek
4. **Wytworzenie modelu** - fusion
5. **Modyfikacja i uproszczenie**
6. **Teksturowanie**
7. **Eksport** (format .obj)

### Czyszczenie skanów
- Usunięcie niepożądanych klatek
- Editor → Eraser (Cutoff-plane, Lasso selection)
- Rozdzielenie na mniejsze części

### Dopasowanie
**Metody:**
- **Rigid** - bez deformacji (preferowane)
- **Nonrigid** - z możliwością deformacji
- Auto-Alignment - automatyczne
- Ręcznie bez punktów charakterystycznych
- Ręcznie z punktami charakterystycznymi

### Rejestracja
- Tools → Registration → Global registration
- Błąd > 0,5 (Spider) lub > 1,2 (Eva) wymaga interwencji

### Fusion (wytworzenie modelu)
**Algorytmy:**
- **Fast fusion** - szybki, zaszumiony
- **Smooth fusion** - dla poruszających się obiektów
- **Sharp fusion** - preferowany, dobra jakość

**Parametry:**
- Resolution (mm)
- Fill_holes (by_radius, watertight, manually)
- Remove_targets

### Modyfikacje
- Small-object filter - usunięcie małych obiektów
- Defeature brush - usuwanie niedoskonałości
- Smoothing - wygładzanie
- Fix holes - wypełnianie dziur
- Mesh simplification - redukcja trójkątów

---

## 9. Formaty 3D

### Format .obj (uniwersalny)
Struktura:
- Plik .obj - struktura siatki trójkątów
- Plik .mtl - powiązanie materiałów z teksturami
- Pliki tekstur (.jpg, .png)

### Inne formaty
- .dwg - AutoCAD
- .3ds - 3ds Max
- .blend - Blender
- .stl - druk 3D (bez koloru/tekstury)
- .amf - CAD z kolorem
- .vrml/.wrl - VR

---

## 10. Muzea Cyfrowe

### Sposoby udostępniania

1. **Kiosk informacyjny** - interaktywne wyświetlacze na wystawie
2. **Wirtualne wycieczki** - panoramy 360°
3. **Katalogi zbiorów** - modele 3D online (np. Sketchfab)
4. **AR** - nakładanie elementów na rzeczywisty obraz

### Redukcja złożoności modeli

**Siatka:**
- Quadric Edge Collapse Decimation (Meshlab)
- Istotne dla przesyłu przez internet

**Tekstura:**
- Rozdzielczość: potęgi 2 (256×256, 1024×1024, 2048×2048, 4096×4096)
- Format .jpg do 30 MB
- Możliwość dodania map połysku (materiały)

**Normal map baking:**
- Przeniesienie szczegółów na teksturę
- Symulacja nierówności na płaskiej powierzchni

### Metody publikacji

1. **Komercyjne serwisy** (Sketchfab)
   - Zalety: wysoka jakość, łatwość
   - Wady: opłaty, licencje

2. **Własny serwis** (threejs.org - WebML)
   - Zalety: niska koszt, pełna kontrola
   - Wady: wymaga wiedzy web

3. **Widok VR**
   - Stereoskopowy widok na urządzeniach mobilnych
   - Wykorzystanie czujników (kompas, pochyłomierz)

---

## 11. Kluczowe definicje do zapamiętania

- **Chmura punktów** - punkty z powierzchni obiektu o znanych współrzędnych x,y,z
- **Skan** - sekwencja klatek z jednego ciągłego ruchu skanera
- **Warunek wodoszczelności** - wszystkie powierzchnie muszą szczelnie przylegać
- **G-kod** - plik z zapisem warstw obiektu do drukowania
- **Slicery** - programy do cięcia modeli 3D
- **FPS** - Frames Per Second (klatki na sekundę)
- **Renderowanie** - proces generowania obrazu 2D ze sceny 3D

---

## Przydatne liczby do zapamiętania

- VR: **90 FPS** - optymalna wartość minimalizująca chorobę lokomocyjną
- Druk 3D: grubość warstwy **0,01-0,2 mm**
- Czas druku obiektu 20 cm: **20-30 godzin**
- Błąd rejestracji Spider: **max 0,5**
- Błąd rejestracji Eva: **max 1,2**
- Tekstury: rozdzielczości **1024-4096 pikseli**

---

## Najważniejsze oprogramowanie

- **Artec Studio 12** - skanowanie
- **Meshlab** - obróbka siatki (darmowe)
- **Blender** - modelowanie (darmowe)
- **3ds Max, Unity 3D, Gimp** - grafika 3D
- **Cura, KISSlicer, MatterControl** - slicery do druku 3D
- **Photoshop** - obróbka tekstur

---

## Wskazówki egzaminacyjne

1. Znaj różnice między VR, AR i MR
2. Pamiętaj główne technologie druku 3D i ich zastosowania
3. Rozumiej proces od skanowania przez obróbkę do eksportu
4. Znaj formaty plików i ich zastosowania
5. Pamiętaj parametry skanerów Artec
6. Rozumiej operacje Boole'a w modelowaniu
7. Znaj techniki modelowania z profili 2D
8. Pamiętaj o warunku wodoszczelności
9. Rozumiej różnicę między grafiką bitmapową a wektorową
10. Znaj zastosowania muzealne technologii 3D
