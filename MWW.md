# Metody Wnioskowania Wielokryterialnego - Skrót do zaliczenia

## 1. PODSTAWOWE POJĘCIA

### 1.1 Funkcje celu
- **Charakteryzują obiekt jako całość** (np. ciężar, sprawność, koszt, estetyka)
- Wyrażone w różnych jednostkach (zł, km, punkty)
- Mogą być **mierzalne** lub **niemierzalne** (skala punktowa)
- Przekształcenie na **kryterium** - określamy czy MAX czy MIN

### 1.2 Zmienne i parametry
- **Zmienne decyzyjne (x)** - podlegają wariancjom w procesie optymalizacji
- **Parametry** - wielkości ustalone wcześniej (stałe)
- **Obszar dopuszczalny X** - wyznaczony przez ograniczenia

### 1.3 Ograniczenia
**Brzegowe:**
- Nakładane na elementy wektora zmiennych: x_i^min ≤ x_i ≤ x_i^max

**Zachowawcze (funkcjonalne):**
- Zależności między zmiennymi i parametrami
- Mogą tworzyć obszary separowane lub puste

### 1.4 Zadanie optymalizacji
**Jednokryterialne:**
```
Znaleźć x* = [x₁*, x₂*, ..., xₘ*]ᵀ
optymalizujące F(x)
przy ograniczeniach: hᵢ(x) = 0, gₖ(x) ≤ 0
```

**Wielokryterialne:**
```
Znaleźć x* = [x₁*, x₂*, ..., xₘ*]ᵀ
optymalizujące F(x) = [F₁(x), F₂(x), ..., Fₙ(x)]ᵀ
przy ograniczeniach: hᵢ(x) = 0, gₖ(x) ≤ 0
```

---

## 2. OPTYMALIZACJA WIELOKRYTERIALNA

### 2.1 Optimum w sensie Pareto (OSP)
**Rozwiązanie x* jest OSP, gdy:**
- Wartość żadnego kryterium nie może być poprawiona bez pogorszenia innego
- Dla każdego j∈J: Fⱼ(x⁻) ≤ Fⱼ(x*) oraz ∃p: Fₚ(x⁻) > Fₚ(x*)

**Synonimy:**
- Rozwiązania niezdominowane, sprawne, efektywne, kompromisowe, Pareto-optymalne

### 2.2 Typy rozwiązań
1. **Dopuszczalne** - spełniają wszystkie ograniczenia
2. **Niezdominowane** - jednoznacznie określone matematycznie (Front Pareto)
3. **Kompromisowe** - wybrane ze zbioru niezdominowanych (np. minimalizacja dystansu)
4. **Reprezentatywne** - często występują w podzbiorach kompromisowych
5. **Preferowane** - wyznaczone ze zbioru niezdominowanych (niejednoznaczne)

### 2.3 Relacje porządku częściowego
**Stożek dodatni:** C₀ = {F = [F₁, ..., Fₙ]ᵀ : Fᵢ ≥ 0 (i = 1, ..., n)}

**Relacja:** Fᵃ <c Fᵇ, jeżeli Fᵇ ∈ CFᵃ

---

## 3. PUNKTY CHARAKTERYSTYCZNE W PRZESTRZENI KRYTERIALNEJ

### 3.1 Punkty narożne (F^n)
- Wyznaczane przez minimalizację każdego kryterium osobno
- Tworzą wektor idealny: F^n_j(x) = F^o_j(x)

### 3.2 Punkt idealny (wektor idealny) F^o
```
F^o(x) = [F^o₁(x), F^o₂(x), ..., F^oₙ(x)]ᵀ
gdzie F^o_j(x) = min{F^j_i(x)} dla każdego kryterium
```
- **Rozwiązanie zazwyczaj fikcyjne**

### 3.3 Punkt antyidealny F^ai
```
F^ai_j(x) = max{F^i_j(x)} dla wszystkich kryteriów
```
- Najmniej preferowany poziom wszystkich celów jednocześnie

### 3.4 Punkt nadir F^na
```
F^na_j(x) = max{F^i_j(x)} z rozwiązań niezdominowanych
```
- Jak antyidealny, ale tylko z rozwiązań Pareto

### 3.5 Punkty referencyjne
- Reprezentują poziom aspiracji/satysfakcji decydenta
- Punkt odniesienia w procedurze porządkowania preferencji

### 3.6 Ocena zadowalająca
- Punkt w przestrzeni kryterialnej: [f₁^S, f₂^S, ..., fⱼ^S]
- Wierzchołek stożka satysfakcji

---

## 4. PROBLEMATYKI DECYZYJNE

### Pα - Problematyka wyboru
```
Zbiór dopuszczalnych A → Podzbiór najlepszych A' + Odrzucone A\A'
```

### Pβ - Problematyka klasyfikacji
```
Zbiór A → Klasa 1, Klasa 2, ..., Klasa p
```

### Pγ - Problematyka porządkowania
```
Zbiór A → Ranking (porządek częściowy lub całkowity)
```

---

## 5. METODY SKALARYZACJI

### 5.1 Rodzaje strategii

**LINIOWE (kompensacyjne):**
1. **Wskaźnik sumacyjny:**
   - Zwykły: F⁺ = Σcⱼ
   - Ważony: F⁺ = Σwⱼcⱼ

2. **Średnia arytmetyczna:**
   - Zwykła: F⁺ = (1/J)Σcⱼ
   - Ważona: F⁺ = (1/J)Σwⱼcⱼ

3. **Ważona długość wektora:**
   - F⁺ = √(Σwⱼcⱼ²) lub F⁺ = √(Σwⱼ²cⱼ²)

**KONIUNKCYJNE (niekompensacyjne):**
1. **Wskaźnik multiplikacyjny:**
   - Zwykły: F⁺ = Πcⱼ
   - Ważony: F⁺ = Πcⱼ^wⱼ lub F⁺ = Π(wⱼcⱼ)

2. **Geometryczna średnia ważona:**
   - F⁺ = ᴶ√(Πwⱼcⱼ)

3. **Wskaźnik paraboliczny:**
   - F⁺ = Π(cⱼ)^αⱼ lub F⁺ = Π(wⱼcⱼ)^αⱼ

**ALTERNATYWNE:**
- F⁺ = Π[j/(eⱼ-Fⱼ)]^αⱼ

### 5.2 Normowanie (kodowanie)

**Cel:** Sprowadzenie wartości do przedziału [0,1] bez jednostek

**Metoda Unitaryzacji Zerowanej (MUZ):**
```
c_ijMUZ = (cᵢⱼ - cᵢⱼmin)/(cᵢⱼmax - cᵢⱼmin)
```

**Inne metody normowania:**
1. **Odchylenie standardowe:**
   - zᵢⱼ = (xᵢⱼ - X̄ⱼ)/S(Xⱼ)

2. **Rozstęp zmiennych:**
   - zᵢⱼ = xᵢⱼ/(max xᵢⱼ - min xᵢⱼ)

3. **Średnia arytmetyczna:**
   - zᵢⱼ = xᵢⱼ/X̄ⱼ

4. **Suma realizacji:**
   - zᵢⱼ = xᵢⱼ/Σxᵢⱼ

5. **Długość wektora:**
   - zᵢⱼ = xᵢⱼ/√[Σxᵢⱼ²]^(1/2)

### 5.3 Kodowanie

**Normowanie względem wartości ekstremalnej:**
- Stymulanty: z'ᵢⱼ = xᵢⱼ/xⱼmax
- Destymulanty: x'ᵢⱼ = 1/xᵢⱼ, potem z'ᵢⱼ = x'ᵢⱼ/x'ⱼmax

**Kodowanie Neumana-Morgensterna:**
- Stymulanty: zᵢⱼ = (xᵢⱼ - xⱼmin)/(xⱼmax - xⱼmin)
- Destymulanty: zᵢⱼ = (xⱼmax - xᵢⱼ)/(xⱼmax - xⱼmin)

**Kodowanie Pattern:**
- Stymulanty: zᵢⱼ = xᵢⱼ/Σxᵢⱼ
- Destymulanty: x'ᵢⱼ = 1/xᵢⱼ, potem zᵢⱼ = x'ᵢⱼ/Σx'ᵢⱼ

### 5.4 Transformacja typów zmiennych

**Destymulanta → Stymulanta:**
- Dane standaryzowane: destymulanta × (-1)
- Dane zunitaryzowane: 1 - destymulanta

**Nominanta → Stymulanta:**
```
zᵢⱼ = {
  1                    dla xᵢⱼ = Nⱼ
  -1                   dla xᵢⱼ < Nⱼ
  (xᵢⱼ - Nⱼ - 1)/(xᵢⱼ - Nⱼ + 1)  dla xᵢⱼ > Nⱼ
}
```

---

## 6. METODY Z RELACJĄ PRZEWYŻSZANIA

### 6.1 Podstawy teoretyczne (Roy)

**Nowe sytuacje preferencyjne:**
- **I** - preferencja równoważności (symetryczna, zwrotna)
- **Q** - preferencja słaba (asymetryczna, przeciwzwrotna)
- **P** - preferencja silna (asymetryczna, przeciwzwrotna)
- **R** - nieporównywalność (symetryczna, przeciwzwrotna)

**Relacje zgrupowane:**
- **N** - brak preferencji (brak P i Q, brak rozróżnienia I i R)
- **J** - przypuszczenie preferencji (aₖQaₗ lub aₖIaₗ)
- **L** - preferencja w szerokim sensie (aₖPaₗ lub aₖQaₗ)
- **K** - preferencja (aₖPaₗ lub aₖRaₗ)
- **S** - przewyższanie (aₖPaₗ lub aₖQaₗ lub aₖIaₗ)

### 6.2 Progi

**Próg równoważności qᵢ[fᵢ(aₖ)]:**
```
0 ≤ fᵢ(aₖ) - fᵢ(aₗ) ≤ qᵢ[fᵢ(aₖ)] ⟹ aₖ Iᵢ aₗ
fᵢ(aₖ) - fᵢ(aₗ) > qᵢ[fᵢ(aₗ)] ∧ fᵢ(aₖ) ≥ fᵢ(aₗ) ⟹ aₖ Lᵢ aₗ
```

**Próg preferencji pᵢ[fᵢ(aₖ)]:**
```
fᵢ(aₖ) - fᵢ(aₗ) > pᵢ[fᵢ(aₖ)] ⟹ aₖ Pᵢ aₗ
0 ≤ fᵢ(aₖ) - fᵢ(aₗ) ≤ pᵢ[fᵢ(aₗ)] ⟹ aₖ Jᵢ aₗ
```

**Próg weta vᵢ[fᵢ(aₗ)]:**
- Odrzuca preferencję nawet przy silnej preferencji dla wszystkich innych kryteriów

**Powiązanie:**
```
f(aₖ) > f(aₗ) ⟹
  - aₖ Iᵢ aₗ  gdy fᵢ(aₖ) - fᵢ(aₗ) ≤ qᵢ[fᵢ(aₗ)]
  - aₖ Qᵢ aₗ  gdy qᵢ[fᵢ(aₗ)] < fᵢ(aₖ) - fᵢ(aₗ) ≤ pᵢ[fᵢ(aₖ)]
  - aₖ Pᵢ aₗ  gdy fᵢ(aₖ) - fᵢ(aₗ) > pᵢ[fᵢ(aₗ)]
```

### 6.3 Metody ELECTRE

**ELECTRE I - Wyznaczenie jądra:**
- Elementy jądra nie przewyższają się wzajemnie
- Każdy element spoza jądra jest przewyższany przez co najmniej jeden element jądra

**ELECTRE II - Dwa preporządki:**
- Etap I: Podział kryteriów na 3 klasy (F₁ przewyższa F₂, odwrotnie, równoważne)
- Etap II: Zliczanie wag w każdej klasie (skalaryzacja wewnętrzna)

**ELECTRE III - Wartościowa relacja przewyższania:**
- Etap I: Indeks zgodności dla każdej pary
- Etap II: Wskaźnik niezgodności dla każdej pary
- Etap III: Stopień przewyższania S(F₁,F₂)
- Etap IV: Preporządek zstępujący i wstępujący
- Etap V: Ranking końcowy (możliwe rozwiązania nieporównywalne)

**ELECTRE IV - Bez wag kryteriów:**
- Mocna i słaba preferencja
- Mocna i słaba relacja przewyższania
- Preporządek jak w ELECTRE III

### 6.4 PROMETHEE (Brans, Mareschal)

**Podstawy:**
- Porównanie parami wariantów
- Różnice dᵢ(aₖ, aₗ) = fᵢ(aₖ) - fᵢ(aₗ)
- Im większa różnica, tym silniejsza preferencja

**Funkcja preferencji:**
```
Gᵢ(aₖ, aₗ) = Fᵢ[dᵢ(aₖ, aₗ)]
Właściwość: Gᵢ(aₖ, aₗ) > 0 ⟹ Gᵢ(aₗ, aₖ) = 0
```

**6 typów uogólnionych kryteriów** (funkcje preferencji)

### 6.5 EXPROM (modyfikacja - Diakoulaki, Koumoutsos)

**Krok 1:** Zagregowany słaby indeks preferencji
```
WP(aᵏ, aˡ) = π(aᵏ, aˡ) = Σⁿᵢ₌₁ wᵢGᵢ(aᵏ, aˡ)
```

**Krok 2:** Zagregowany ścisły indeks preferencji
```
SP(aᵏ, aˡ) = Σⁿᵢ₌₁ wᵢSPᵢ(aᵏ, aˡ)
```

**Krok 3:** Całkowity indeks preferencji
```
TP(aᵏ, aˡ) = min{1; WP(aᵏ, aˡ) + SP(aᵏ, aˡ)}
```

**Krok 4:** Dodatni i ujemny przepływ przewyższania
```
φ⁺(aᵏ) = 1/(m-1) Σᵐₗ₌₁ TP(aᵏ, aˡ)
φ⁻(aᵏ) = 1/(m-1) Σᵐₗ₌₁ TP(aˡ, aᵏ)
```

**Krok 5:** Przepływ netto
```
φ(aᵏ) = φ⁺(aᵏ) - φ⁻(aᵏ)
```

### 6.6 MAPPAC (Matarazzo)

- Macierz preferencji i równoważności
- Progi preferencji dla każdego kryterium
- Bazowe wskaźniki preferencji dla par rozwiązań i kryteriów
- Zagregowana macierz preferencji
- Indeks końcowy dla każdego rozwiązania
- Ranking (największy indeks = pierwsze miejsce)

### 6.7 ORESTE (Roubens)

- Preporządek zupełny dla kryteriów
- Progi preferencji, równoważności, nieporównywalności
- Test równoważności i nieporównywalności
- Zamiana preporządku na rangi
- Macierz intensywności preferencji
- Ranking końcowy

---

## 7. METODA ANALIZY GRUPOWEJ - BLIN

**Cel:** Agregacja uporządkowań preferencyjnych grupy decydentów

**Dane:**
- A = {a₁, ..., aₘ} - zbiór decyzji
- B = {b₁, ..., bₙ} - zbiór decydentów
- Oₖ ⊂ A × A - uporządkowanie k-tego decydenta

**Procedura:**
1. **Macierz preferencji Sₖ** dla każdego decydenta (wartości 0 lub 1)
2. **Macierz sumaryczna:** N = Σₖ₌₁ⁿ Sₖ
3. **Preferencja społeczna (rozmyta):** μᴿ(aᵢ, aⱼ) = nᵢⱼ/n
4. **α-obcięcie:** Rₜ = {(aᵢ, aⱼ): μᴿ(aᵢ, aⱼ) ≥ t}

**Przykład:**
- Jeśli wszyscy decydenci: a > b ⟹ μᴿ(a, b) = 1
- Jeśli 70% decydentów: a > b ⟹ μᴿ(a, b) = 0,7

---

## 8. METODA AHP (Analytic Hierarchy Process - Saaty)

### 8.1 Charakterystyka
- Uwzględnia wpływ psychiki człowieka
- Bazuje na obliczeniach matematycznych
- Hierarchiczna struktura problemu
- Porównania parami

### 8.2 Skala ocen Saaty'ego

| Nota | Opis | Dominacja |
|------|------|-----------|
| 1 | Równoważność | brak |
| 3 | Słaba przewaga | słaba |
| 5 | Umiarkowana przewaga | umiarkowana |
| 7 | Silna przewaga | silna |
| 9 | Absolutna przewaga | absolutna |
| 2,4,6,8 | Wartości pośrednie | - |

### 8.3 Procedura (4 fazy)

**Faza 1: Hierarchiczna struktura**
- Cel nadrzędny
- Kryteria i podkryteria
- Warianty decyzyjne

**Faza 2: Określenie preferencji**
- Porównanie parami kryteriów (macierz)
- Porównanie parami wariantów dla każdego kryterium
- Skala {1/9, 1/8, ..., 1/2, 1, 2, ..., 8, 9}

**Faza 3: Normalizacja i wektory własne**
- Normalizacja macierzy porównań
- Obliczenie wektorów skali (średnie arytmetyczne kolumn)
- Badanie globalnej spójności (CR < 0,10)

**Faza 4: Obliczenie użyteczności**
```
Ocena wariantu = Σ(ocena w kryterium × waga kryterium)
```

**Przykład obliczeniowy:**
- Normalizacja: suma kolumny → dzielenie każdego elementu
- Wektor skali: średnia arytmetyczna wierszy znormalizowanej macierzy
- Ocena końcowa: iloczyn skalarny wektorów ocen i wag

---

## 9. METODY LEKSYKOGRAFICZNE I HIERARCHICZNE

### 9.1 Metoda leksykograficzna

**Założenia:**
- Hierarchia kryteriów (uporządkowanie ważności)
- Wartości liczbowe kryteriów
- Brak kompensacji między kryteriami

**Procedura:**
1. Uporządkowanie kryteriów wg ważności: F₄ > F₂ > F₅ > F₁ > F₃
2. Optymalizacja wg najważniejszego kryterium (F₄)
3. Wybór rozwiązań o wartościach MAX/MIN
4. Jeśli jedno rozwiązanie → KONIEC
5. Jeśli wiele → optymalizacja wg kolejnego kryterium (F₂)
6. Powtarzanie aż do jednego rozwiązania lub wyczerpania kryteriów

**Uwaga:** Zmiana hierarchii kryteriów zmienia wynik!

### 9.2 Metoda optymalizacji hierarchicznej

**Modyfikacja:** Wprowadzenie dopuszczalnych odchyleń ε

**Ograniczenie dodatkowe:**
```
fᵢ₋₁(X) ≤ (1 ± εᵢ₋₁) · fᵢ₋₁(xᵢ₋₁)
```

- ε = 0 → metoda leksykograficzna
- ε > 0 → metoda mniej restrykcyjna
- Procedura identyczna jak w metodzie leksykograficznej

### 9.3 Zmodyfikowana metoda leksykograficzna

**Cel:** Wyznaczenie rankingu (nie tylko jednego rozwiązania)

**Procedura:**
1. Ustalenie hierarchii kryteriów
2. Wyznaczenie pierwszego rozwiązania optymalnego (1. miejsce)
3. Usunięcie tego rozwiązania ze zbioru
4. Wyznaczenie kolejnego rozwiązania (2. miejsce)
5. Powtarzanie aż do wyczerpania wariantów

---

## 10. INNE METODY

### 10.1 Metoda ograniczonych kryteriów (Trade-Off)

**Idea:**
- Ustalenie poziomów εᵢ dla kryteriów
- Optymalizacja względem wybranego kryterium fᵢ
- Pozostałe kryteria jako ograniczenia: fⱼ(X) ≥ εⱼ

```
fᵢ(X) → MIN
fⱼ(X) ≥ εⱼ (i = 1,...,M; i ≠ r)
gₖ(X) ≤ 0 (k = 1,...,K)
hⱼ(X) = 0 (j = 1,...,J)
```

### 10.2 Metoda kryterium globalnego (Global Criterion)

**Funkcja celu:**
```
[Σ|fᵢ(X*) - fᵢ(X)|ᴾ / fᵢ(X*)]^(1/P) → MIN
```

- P ∈ (1, 2) - najczęściej
- Poszukujemy rozwiązania bliskiego f(X*)

### 10.3 Metoda funkcji odległości (Distance Function)

**Minimalizacja:**
```
Σ[(fᵢ(X*) - fᵢ(X)) / fᵢ(X*)]ᴾ → MIN
```

**Dla P → ∞ (Metoda Min-Max):**
```
MAX[wᵢ · (fᵢ(X*) - fᵢ(X)) / fᵢ(X*)] → MIN
```

### 10.4 Metoda Mini-Maxu

**Minimalizacja:**
```
[MAX|(fᵢ(X*) - fᵢ(X)) / fᵢ(X*)|]ᴾ → MIN
```

- Dla P = 2 → minimalizacja odległości między rozwiązaniem przybliżonym a optymalnym

### 10.5 Metoda TOPSIS (Hwang, Masuda)

**Idea:**
- Najbliżej punktu idealnego y^id
- Najdalej od punktu antyidealnego y^ai
- Normalizacja wektorowa (zamiast liniowej)

**Wskaźnik:**
```
fᵢ(yₙᴰ) = MIN[dᵢ / (dᵢᵢ + dₐᵢ)]
```

gdzie:
- dᵢᵢ = |yₙᴰ - y^id| - odległość od idealnego
- dₐᵢ = |yₙᴰ - y^ai| - odległość od antyidealnego

### 10.6 Metoda funkcji użyteczności

**Globalna funkcja użyteczności (postać addytywna):**
```
U(x) = Σᵐᵢ₌₁ uᵢ(gᵢ(x))
```

gdzie:
- m - liczba kryteriów
- gᵢ(x) - wartość wariantu x na i-tym kryterium
- uᵢ(gᵢ(x)) - funkcja użyteczności cząstkowej

**Właściwości:**
- Agregacja wszystkich kryteriów do jednej wartości
- Wariant o lepszej użyteczności jest preferowany (xPy)
- Nierozróżnialne dla tej samej wartości (xIy)
- **Użyteczność NIE jest sumą wartości kryteriów!**

**Dopasowanie:**
- Dobór współczynników liniowych funkcji
- Odtworzenie rankingu wybranego przez decydenta
- Współczynnik Kendalla (zgodność): [-1, 1]
  - 1 = pełna zgodność
  - -1 = brak zgodności

---

## 11. PODSUMOWANIE METOD

### Podział ze względu na podejście:

**1. Metody syntezy do pojedynczego kryterium (skalaryzacja):**
- Normowanie, kodowanie
- Strategia liniowa, koniunkcyjna, alternatywna
- Metoda AHP
- Metoda funkcji użyteczności

**2. Metody z relacją przewyższania:**
- ELECTRE I, II, III, IV
- PROMETHEE, EXPROM
- MAPPAC, ORESTE

**3. Metody leksykograficzne i hierarchiczne:**
- Metoda leksykograficzna (klasyczna i zmodyfikowana)
- Metoda optymalizacji hierarchicznej

**4. Metody interaktywne:**
- Metoda ograniczonych kryteriów
- Metoda kryterium globalnego
- Metoda funkcji odległości, Mini-Max, TOPSIS

---

## 12. NAJWAŻNIEJSZE WZORY DO ZAPAMIĘTANIA

### Normalizacja MUZ:
```
c_ijMUZ = (cᵢⱼ - cᵢⱼmin) / (cᵢⱼmax - cᵢⱼmin)
```

### Kodowanie N-M (stymulanty):
```
zᵢⱼ = (xᵢⱼ - xⱼmin) / (xⱼmax - xⱼmin)
```

### Wskaźnik ważony sumacyjny:
```
F⁺ = Σwⱼcⱼ  (gdzie Σwⱼ = 1)
```

### Punkt idealny:
```
F^o_j(x) = min{F^j_i(x)} dla każdego j
```

### Optimum Pareto:
```
x* jest OSP ⟺ ∄x⁻: Fⱼ(x⁻) ≤ Fⱼ(x*) ∀j ∧ ∃p: Fₚ(x⁻) > Fₚ(x*)
```

### AHP - ocena wariantu:
```
Ocena = Σⁿⱼ₌₁ (ocena_wariantu_w_kryterium_j × waga_kryterium_j)
```

---

## 13. WSKAZÓWKI DO EGZAMINU

### Co musisz umieć:
1. ✅ **Rozróżnić typy problemów** (Pα, Pβ, Pγ)
2. ✅ **Wyznaczyć Front Pareto** (graficznie i analitycznie)
3. ✅ **Znormalizować/zakodować dane** (MUZ, N-M, Pattern)
4. ✅ **Obliczyć wskaźniki skalaryzacyjne** (sumacyjny, multiplikacyjny)
5. ✅ **Zastosować metodę AHP** (porównania parami, normalizacja, wagi)
6. ✅ **Zrozumieć różnicę między metodami** (skalaryzacja vs relacje przewyższania)
7. ✅ **Transformować typy zmiennych** (destymulanta→stymulanta)
8. ✅ **Znać punkty charakterystyczne** (idealny, nadir, antyidealny)
9. ✅ **Rozumieć progi w metodach przewyższania** (q, p, v)
10. ✅ **Zastosować metodę leksykograficzną** (uporządkowanie kryteriów)

### Typowe pytania:
- Czym różni się rozwiązanie dopuszczalne od niezdominowanego?
- Co to jest optimum w sensie Pareto?
- Jakie są główne rodzaje strategii skalaryzacji?
- Wymień metody normowania i ich zastosowanie
- Opisz metodę AHP krok po kroku
- Czym różnią się metody ELECTRE od PROMETHEE?
- Co to jest punkt idealny i nadir?
- Kiedy stosujemy metodę leksykograficzną?
- Jakie są wady i zalety skalaryzacji?
- Czym charakteryzują się metody z relacją przewyższania?

### Mnemotechnika:
- **PINAR** - Punkty: **I**dealny, **N**adir, **A**ntyidealny, **R**eferencyjny, na**R**ożne
- **3P** - Problematyki: **P**α (wybór), **P**β (klasyfikacja), **P**γ (porządkowanie)
- **LKA** - Strategie: **L**iniowa, **K**oniunkcyjna, **A**lternatywna
- **QPR** - Progi: **Q** (równoważności), **P** (preferencji), **R** (weta - nie mylić z relacją!)

---

**Powodzenia na zaliczeniu!** 🎓
