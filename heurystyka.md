# Strategia podejścia do egzaminu "Systemy Sztucznej Inteligencji"

## Kontekst

Egzamin zawiera pytania wielokrotnego wyboru (zazwyczaj 5 opcji). Ocena **all-or-nothing** -
punkt tylko za zaznaczenie WSZYSTKICH poprawnych i ŻADNEJ niepoprawnej.

Analiza 157 pytań z banku ujawniła silne wzorce wskazujące na generowanie przez LLM.

---

## Wyniki symulacji heurystyki (bez wiedzy merytorycznej)

| Strategia | Wynik | Procent |
|-----------|:-----:|:-------:|
| Losowo (zawsze 2 z 5) | 7.8 / 157 | **5.0%** |
| Losowo (znając liczbę poprawnych) | 33.0 / 157 | **21.0%** |
| Sama heurystyka (wzorce formalne) | 38 / 157 | **24.2%** |
| Heurystyka - trafność na poziomie opcji | 549 / 779 | **70.5%** |
| Heurystyka - "prawie trafione" (off-by-one) | 81 / 157 | **51.6%** |

Sama heurystyka daje ~24% dokładnych trafień, ale na poziomie pojedynczych opcji
**poprawnie klasyfikuje 70.5%** odpowiedzi. Problem to surowe all-or-nothing.

---

## Strategia krok po kroku

### KROK 1: Określ ile odpowiedzi jest poprawnych

To kluczowy bottleneck (42.7% trafień heurystyki).

| Zakładana liczba | Szansa | Jak rozpoznać |
|:----------------:|:------:|---------------|
| **2** | **49.7%** pytań | Domyślna - stosuj gdy nie masz pewności |
| **1** | **31.8%** pytań | Pytania "Która definicja NAJLEPIEJ...", "Co NAJLEPIEJ opisuje...", "Co zwróci...", "Jaka jest wartość..." |
| **5** | **5.7%** pytań | Pytania typu "Dopasuj X do Y" / "Przyporządkuj" - wszystkie pary prawidłowe |
| **3** | **9.6%** pytań | Rzadkie - gdy 3 opcje wyraźnie merytoryczne, 2 absurdalne |
| **0** | **1.9%** pytań | Pytania "Wskaż NIEPOPRAWNE/FAŁSZYWE" gdzie wszystkie opcje są fałszywe |

**Zasada:** Jeśli pytanie pyta o "najlepszą" jedną rzecz → 1. Jeśli "dopasuj/przyporządkuj" → 5. Reszta → 2.

### KROK 2: Eliminuj oczywiste dystraktory

Szukaj tych **red flags** - opcja prawie na pewno NIEPOPRAWNA, jeśli zawiera:

**Absolutyzmy (nadreprezentacja 5-10x w fałszywych):**
- "zawsze" / "nigdy"
- "wyłącznie" / "tylko"
- "gwarantuje"
- "niezależnie od..."
- "identyczny z..."
- "musi być"
- "zabronione"
- "nie może" / "nie istnieje"
- "każdy" / "żaden"

**Off-topic / absurdy:**
- Renderowanie, GPU, CPU, animacja
- Szyfrowanie, kompresja, serializacja
- Sortowanie, rzut monetą
- Format pliku, PDF, ZIP
- Kolor interfejsu, GUI
- Teleportacja, memy

**~30% nieprawidłowych opcji** zawiera co najmniej jeden z tych markerów.

### KROK 3: Z pozostałych wybierz N najlepszych

Prawidłowa odpowiedź z dużym prawdopodobieństwem:
- Jest **najdłuższa / najbardziej szczegółowa** (72% pytań - najdłuższa opcja jest poprawna)
- Zawiera **nawiasy, przykłady** ("np.", "np.:", "np. x, y")
- Zawiera **kwalifikatory**: "może", "zwykle", "często", "w zależności od"
- Zawiera **strzałki** (→) i **ukośniki** (/) wskazujące na dopasowania
- Zawiera **konkretne nazwy** (algorytmów, metod, klas Pythona)

### KROK 4: Sprawdź pozycje (dodatkowa wskazówka)

Dla pytań z 2 poprawnymi odpowiedziami, najczęstsze pary pozycji:
- **(1, 5)** - 16.9% (1.7x powyżej oczekiwanej) - "kanapka"
- **(1, 4)** - 13.0% (1.3x)
- **(1, 2)** - 11.7% (1.2x)

**48% pytań z 2 poprawnymi** ma pozycję 1 jako jedną z nich.

---

## Rozbicie skuteczności heurystyki wg typu pytania

| Typ pytania (wg liczby poprawnych) | Trafień heurystyką | Szanse |
|:-:|:-:|:-:|
| 2 poprawne (78 pytań) | 30 / 78 | **38.5%** |
| 1 poprawna (50 pytań) | 8 / 50 | **16.0%** |
| 3 poprawne (15 pytań) | 0 / 15 | **0.0%** |
| 5 poprawnych (9 pytań) | 0 / 9 | **0.0%** |
| 0 poprawnych (3 pytania) | 0 / 3 | **0.0%** |

**Wniosek:** Heurystyka działa najlepiej na pytaniach z 2 poprawnymi (najczęstszy typ).
Pytania z 1, 3 lub 5 poprawnymi wymagają wiedzy merytorycznej.

---

## Optymalna strategia łączona: heurystyka + wiedza

### Scenariusz A: Znasz odpowiedź → odpowiadaj wiedzą
Heurystykę stosuj TYLKO jako sanity check.

### Scenariusz B: Nie znasz odpowiedzi, ale rozumiesz tematykę
1. Wyeliminuj opcje z absolutyzmami/absurdami
2. Z pozostałych wybierz najbardziej szczegółowe
3. Domyślnie zaznacz 2

### Scenariusz C: Kompletnie nie znasz tematu
1. Odrzuć najkrótsze i absurdalne
2. Zaznacz 2 najdłuższe odpowiedzi
3. Jeśli w wątpliwości - pozycje (1, 5) lub (1, 4) jako fallback

---

## Szacowane szanse zdania

Założenia do kalkulacji:
- Egzamin ma **Seed** → losuje podzbiór z banku 157 pytań (np. 30-40)
- Próg zdawalności: typowo 50-60%

| Scenariusz | % trafień | Przy 30 pytaniach | Przy 40 pytaniach |
|------------|:---------:|:-----------------:|:-----------------:|
| Sama heurystyka (0 wiedzy) | ~24% | ~7 pkt | ~10 pkt |
| Heurystyka + powierzchowna wiedza (~50% tematów) | ~40-45% | ~12-14 pkt | ~16-18 pkt |
| Heurystyka + dobra wiedza (~70% tematów) | ~60-65% | ~18-20 pkt | ~24-26 pkt |
| Heurystyka + bardzo dobra wiedza (~85% tematów) | ~75-80% | ~23-24 pkt | ~30-32 pkt |

**Sama heurystyka nie wystarczy do zdania** (24% < 50% próg).
Ale jako **wspomaganie** przy częściowej wiedzy podnosi wynik o ~10-15 p.p.

---

## Szybka ściąga (cheat sheet na egzamin)

```
ELIMINUJ jeśli widzisz:
  "zawsze" "nigdy" "wyłącznie" "tylko" "gwarantuje"
  "niezależnie" "identyczny" "zabronione" "musi"
  absurdy niezwiązane z tematem

WYBIERAJ:
  - Najdłuższą / najbardziej szczegółową opcję
  - Opcje z nawiasami, przykładami, "np."
  - Opcje z kwalifikatorami: "może", "zwykle", "często"

DOMYŚLNIE:
  - Zaznacz 2 odpowiedzi
  - "Najlepiej opisuje..." / "Co zwróci..." → zaznacz 1
  - "Dopasuj" / "Przyporządkuj" → zaznacz 5

W RAZIE WĄTPLIWOŚCI:
  - Pozycja 1 + pozycja 5 (najczęstsza para)
  - Pozycja 1 + pozycja 4 (druga najczęstsza)
```

---

## Ważne zastrzeżenie

Ta analiza dotyczy konkretnego banku pytań. Jeśli prowadzący zmodyfikuje pytania
(dłuższe dystraktory, usunięcie absolutyzmów, wyrównanie długości), heurystyka
przestanie działać. Strategia jest uzupełnieniem nauki, nie jej zamiennikiem.
