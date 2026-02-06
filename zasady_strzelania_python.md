# Analiza wzorców odpowiedzi - egzamin "Systemy Sztucznej Inteligencji"

**Plik źródłowy:** `AllExam_SystemySztucznejInteligencji.txt`
**Liczba pytań:** 156
**Format:** wielokrotnego wyboru, zazwyczaj 5 opcji

---

## 1. Najdłuższa odpowiedź = prawidłowa

To najsilniejszy sygnał generowania przez AI:

- **72% pytań** ma najdłuższą opcję oznaczoną jako prawidłowa
- Prawidłowe odpowiedzi są średnio **1.33x dłuższe** niż nieprawidłowe
- Odpowiedzi >100 znaków: **13.2% prawidłowych** vs **0.4% nieprawidłowych** (33x różnica!)
- Prawidłowe odpowiedzi częściej zawierają nawiasy, przykłady ("np."), hedging

| Metryka | Prawidłowe | Nieprawidłowe | Stosunek |
|---------|:----------:|:-------------:|:--------:|
| Średnia długość (znaki) | 67.9 | 50.9 | **1.33x** |
| Mediana długości (znaki) | 68 | 53 | 1.28x |
| Średnia liczba słów | 8.8 | 6.7 | **1.31x** |
| % z 81+ znakami | 30.4% | 5.1% | **6.0x** |
| % z 101+ znakami | 13.2% | 0.4% | **33.0x** |

Sam wybór najdłuższej odpowiedzi dałby zdawalność znacznie powyżej losowej.

---

## 2. Nieprawidłowe odpowiedzi omijają tematykę

Dystraktory często są absurdalnie nie na temat, np.:

- Pytanie o ML → "Renderowanie grafiki 3D"
- Pytanie o sieci neuronowe → "Sortowanie próbek w partii danych"
- Pytanie o regresję → "Serializacja modelu do formatu obrazu"
- Pytanie o funkcję straty → "Losowo zmienia etykiety"
- Pytanie o drzewa decyzyjne → "Funkcja aktywacji sigmoidalna"

To klasyczny fingerprint LLM - generuje "oczywiste bzdury" zamiast trudnych, wiarygodnych dystraktorów.

---

## 3. Słowa-klucze w fałszywych odpowiedziach

Nieprawidłowe odpowiedzi masowo używają absolutystycznego języka:

| Słowo | W nieprawidłowych | W prawidłowych | Nadreprezentacja |
|-------|:-----------------:|:--------------:|:----------------:|
| "zawsze" | 9.3% | 1.7% | **5.5x** |
| "wyłącznie" | 6.1% | 0.7% | **8.7x** |
| "niezależnie" | 3.0% | 0.3% | **10x** |
| "gwarantuje" | 1.7% | 0.3% | **5.7x** |
| "identyczny" | 1.7% | 0.3% | **5.7x** |
| "bez" | 9.7% | 2.0% | **4.9x** |
| "tylko" | 3.2% | 0.7% | **4.6x** |
| "losow-" | 4.9% | 2.0% | **2.5x** |
| "musi" | 1.1% | 0.0% | **∞** |

**30% nieprawidłowych** odpowiedzi zawiera co najmniej jedno z tych słów.

**Zasada:** jeśli opcja twierdzi, że coś "zawsze", "nigdy", "wyłącznie" lub "gwarantuje" - prawie na pewno jest fałszywa.

---

## 4. Monotonny schemat liczby poprawnych odpowiedzi

| Liczba poprawnych | Liczba pytań | Procent |
|:-----------------:|:------------:|:-------:|
| 0 | 3 | 1.9% |
| 1 | 50 | 32.1% |
| 2 | 77 | **49.4%** |
| 3 | 15 | 9.6% |
| 4 | 2 | 1.3% |
| 5 | 9 | 5.8% |

- **49.4% pytań** ma dokładnie 2 poprawne odpowiedzi (na 5 opcji)
- **81.4%** ma 1 lub 2 poprawne
- Występują ciągi 7-8 kolejnych pytań z identyczną liczbą poprawnych:
  - Q13-19: 7 kolejnych z dokładnie 2 poprawnymi
  - Q21-28: 8 kolejnych z dokładnie 2 poprawnymi
  - Q112-118: 7 kolejnych z dokładnie 1 poprawną
- Blok "Czyszczenie danych" (Q16-28): **12 z 13** pytań ma dokładnie 2 poprawne

To wskazuje na generowanie wsadowe z promptem typu "wygeneruj 5 opcji, oznacz 2 jako poprawne".

---

## 5. Wzorzec pozycji (1,5) - "kanapka"

W pytaniach z 2 poprawnymi odpowiedziami, najczęstsze pary pozycji:

| Para pozycji | Liczba | Oczekiwana | Odchylenie |
|:------------:|:------:|:----------:|:----------:|
| **(1, 5)** | **13** | 7.7 | **+69%** |
| (1, 4) | 10 | 7.7 | +30% |
| (1, 2) | 9 | 7.7 | +17% |
| (3, 4) | 8 | 7.7 | +4% |
| (3, 5) | 8 | 7.7 | +4% |

AI "otacza" błędne odpowiedzi poprawnymi na krańcach. **48.1%** pytań dwu-poprawnych zawiera pozycję 1 jako jedną z poprawnych.

---

## 6. Pytania-anomalie

### Wszystkie opcje poprawne (5/5) - 9 pytań
Q5, Q7, Q29, Q39, Q40, Q52, Q62, Q64, Q65 - klastrują się w pary/trójki, co wskazuje na generowanie wsadowe.

### Zero poprawnych (0/5) - 3 pytania
Q35, Q41, Q50 - wszystkie opcje pełne absolutyzmów ("wymaga", "zawsze", "wyłącznie", "zabroniona"). AI miało problem z wygenerowaniem wiarygodnych prawdziwych stwierdzeń obok fałszywych.

---

## 7. Asymetria szczegółowości

| Metryka | Prawidłowe | Nieprawidłowe |
|---------|:----------:|:-------------:|
| Z nawiasami | 27.2% | 15.7% |
| Z "np." (przykład) | 5.0% | 1.5% |

Prawidłowe odpowiedzi są zniuansowane, z przykładami i kwalifikacjami. Nieprawidłowe są krótkie i kategoryczne.

---

## 8. Różnice między blokami tematycznymi

| Blok tematyczny | Śr. poprawnych | Uwagi |
|-----------------|:--------------:|-------|
| Przeszukiwanie/Planowanie (Q53-65) | 2.62 | Trzy pytania 5/5 |
| Definicje SI (Q1-7) | 2.57 | Dwa pytania 5/5 |
| Zbiory rozmyte/OWA (Q131-143) | 2.23 | |
| Detekcja anomalii (Q144-156) | 2.15 | 11 pytań z dokładnie 2 |
| Podstawy ML (Q29-39) | 2.09 | |
| Czyszczenie danych (Q16-28) | 1.92 | 12/13 pytań z dokładnie 2 |
| Regresja (Q79-91) | **1.54** | 8 pytań jednopoprawnych |
| Klasyfikacja (Q105-117) | **1.46** | 7 jednopoprawnych |

---

## Podsumowanie - strategia "zdawania na wzorcach"

1. **Wybierz najdłuższą/najbardziej szczegółową opcję** → ~72% trafność
2. **Odrzuć opcje z "zawsze/nigdy/wyłącznie/gwarantuje"** → eliminujesz ~30% fałszywych
3. **Odrzuć odpowiedzi absurdalnie nie na temat** → eliminujesz kolejne dystraktory
4. **Domyślnie zakładaj 2 poprawne z 5** → trafiasz w schemat ~50% pytań

---

## Werdykt

Egzamin jednoznacznie nosi cechy generowania przez duży model językowy (LLM) z powtarzalnym promptem i minimalną redakcją ludzką. Kluczowe dowody:

1. **Korelacja długości z poprawnością** - w dobrze zaprojektowanym egzaminie nie powinna występować
2. **Formulaiczne dystraktory** - absolutystyczny język zamiast wiarygodnych błędnych odpowiedzi
3. **Monotonna struktura** - niemal połowa pytań w schemacie 2/5
4. **Dystraktory nie na temat** - absurdalne opcje zamiast trudnych, ale bliskich tematowi
5. **Generowanie wsadowe** - widoczne w klastrach pytań o identycznej strukturze
