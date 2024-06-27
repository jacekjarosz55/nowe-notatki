> **Kompresja może zastąpić mieszanie na terminie pierwszym!**
# Wstęp do kompresji

Kompresja to *sposób kodowania*, który polega na zmniejszeniu ilości pamięci do przechowania danych.

## Algorytmy kompresji

**Kompresja danych** - Zmiana sposobu zapisu informacji tak, aby zmniejszyć redundancję i tym samym objętość zbioru, nie zmieniając przenoszonych informacji (przy kompresji stratnej, zachowując istotne informacje).

Działaniem przeciwnym do kompresji jest **dekompresja**.

Kompresję dzielimy na:
- **bezstratną** - można odzyskać identyczną postać pierwotną.
- **stratną** - odzyskanie 1:1 jest niemożliwe. Zachowywane są tylko istotne informacje zawarte w danych (zwykle różnica nie powinna być łatwo zauważalna)

### Przykład kompresji bezstratnej:
Jeśli jakaś dana się powtarza wiele razy, np. "bbbbaaaaa", możemy to zapisać jako np. "4b5a".

## Współczynnik kompresji

$$k = \frac{l_{WE} - l_{WY}}{l_{WE}}$$
Gdzie $l_{WE}$ - długość zbioru wejściowego, $l_{WY}$ - długość zbioru wyjściowego.

Jest to wartość od $0..1$, gdzie tym bliżej $1$, tym bardziej zmniejszona została długość zbioru (mamy **zysk**), $1$ jest niemożliwe (długość wyjściowa byłaby równa $0$), a $0$ oznacza że długość została taka sama (dane **nie zostały skompresowane**), wartość ujemna oznacza że długość wyjściowa jest większa niż długość wejściowa (mamy **stratę**)(uwaga: to *nie* jest kompresja stratna, oczywiście).
## Rodzaje kompresji
- RLE - kodowanie długości serii (Run Length Encoding) ("bbbbaaaaa" -> "4b5a")
- Algorytm Huffmana - metoda statystyczna
- LZ77, LZ78, LZW - metody słownikowe (spis dłuższych słów do których się odwołujemy mniejszymi kluczami)

### RLE - kodowanie długości serii (Run Length Encoding) 

"AAAABCDDDDD" - > "4a1b1c5d"


Pamiętamy żeby zawsze było to jednoznaczne (nie możemy mieszać różnic)
"11112344444"  -> "41121354"

aby uniknąć problemu z kompresją pojedynczych znaków, użyjemy negatywnej wartości żeby oznaczyć ile *różnych wartości* będzie następowało po sobie:
"11112344444" -> "41-22354"

"AAAABCDDDDD" -> "4A-2BC5D"
Jeżeli jest mało krótkich serii w kodzie, ta metoda może przynieść stratę


16 1 -2 3 4 7 11 = po kompresji

Ciąg wyjściowy: 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 3 4 11 11 11 11 11 11 11

Zły przykład: "MAMAMAMAK" - nie ma wielu elementów obok siebie, nie możemy skompresować tego dobrze używając RLE

Przykład kompresji o współczynniku $k = 0$:
"AA" -> "2A"

## Algorytm Huffmana

###  Określ prawdopodobieństwo (lub częstość występowania każdego symbolu z S)
Powiedzmy że mamy znane najbardziej prawdopodobne liczby, budujemy z nich drzewo.

"AAABBBCAAABCDAAAAAEBEBBCEDDDAEFF"

Występowanie: A-12, b-7, C-3, D-4, E-4, F-2

**!! Wybieramy elementy występujące najrzadziej i je grupujemy wspólnym korzeniem**

Elementy o mniejszej częstotliwości - na prawo

1. A-12, B-7, C-3, D-4, E-4, F-2
2. A-12, B-7, D-4, E-4, **FC-5**
2. A-12, B-7, D-4, E-4, **FC-5**

Później ustawiamy np. 0 dla lewych gałęzi  a 1 dla prawych korzeni
a=>0
d=>100
E=>101
f=>1100
C=>1101
B=>111

przykład: 
ABCE - rozmiar = 8 * 4 = 32 bitów
zakodowane: 01111101101 - rozmiar 11bitów

Możemy to obliczyć po prostu mnożąc ilość bitów zakodowanej każdej z liter przez ich występowanie




Dla algorytmu Huffmana musimy przechować drzewo które stworzymy, dlatego może być on nieodpowiedni dla tekstów mniejszych (lub o mniejszej różnorodności znaków).

Możemy stworzyć drzewo Huffmana nie tylko częstotliwością występowania



## Lempel-Ziv 77 (LZ77)
Metoda bezstratnej kompresji słownikowej.
Wykorzystuje fakt, że poszczególne słowa powtarzają się w bloku danych.

Tworzymy słownik na bieżąco z tekstu wejściowego:



LZ77 korzysta z **bufora (okna)**:
- bufor słownikowy (słownik) - przechowujący k ostatnio przetwarzanych symboli
- bufor wejściowy (lub bufor kodowania), przechowujący n symboli do zakodowania


Przykład:

> Uwaga: słowniki i bufory zwykle są dużo większe.

Dla tekstu: "AAABBBCAAABCDAAAAAEBEBBCEDDDAEFF"

(0, 3, B) - od pozycji 0, 3 znaki są zgodne, następne jest B (potem przesuwamy 'za' to B)

| słownik             | bufor             | reszta                       | wyjście   |
| ------------------- | ----------------- | ---------------------------- | --------- |
| AAAAAA              | AAAB              | BBCAAABCDAAAAAEBEBBCEDDDAEFF | A         |
| <mark>AAA</mark>AAA | <mark>AAA</mark>B | BBCAAABCDAAAAAEBEBBCEDDDAEFF | (0, 3, B) |
| AAAAA<mark>B</mark> | <mark>BB</mark>CA | AABCDAAAAAEBEBBCEDDDAEFF     | (5, 2, C) |
| <mark>AA</mark>BBBC | <mark>AA</mark>AB | CDAAAAAEBEBBCEDDDAEFF        | (0, 2, A) |
| BBCAAA              | BCDA              | AAAAEBEBBCEDDDAEFF           |           |
|                     |                   |                              |           |
I tak dalej.

Wynik: A 0 3 B 5 2 C 0 2 A....

znając wielkość okienka słownika oraz bufor możemy dekompresować tekst 

Dla tekstu: "AAABBBCAAABCDAAAAAEBEBBCEDDDAEFF" wynik to "A03B52C02A12D03A21E00B42B00C01D52A11F51" (współczynnik kompresji $k= (32-39)/32$ !!!)

## LZ78

| we   | wy     | słownik(indeks, słowo) | Notatki                                                              |
| ---- | ------ | ---------------------- | -------------------------------------------------------------------- |
| A    | (0,A)  | 1, A                   | Nie ma nic w słowniku (0, A)                                         |
| AA   | (1,A)  | 2, AA                  | Zapisuję słowo ze słownika indeks #1 (1, A), dopisuję AA do słownika |
| B    | (0,B)  | 3,B                    |                                                                      |
| BB   | (3,B)  | 4, BB                  |                                                                      |
| C    | (0,C)  | 5,C                    |                                                                      |
| AAA  | (2,A)  | 6,AAA                  |                                                                      |
| BC   | (3,C)  | 7, BC                  |                                                                      |
| D    | (0,D)  | 8,D                    |                                                                      |
| AAAA | (6,A)  | 9,AAAA                 |                                                                      |
| AE   | (1,E)  | 10,AE                  |                                                                      |
| BE   | (3,E)  | 11,BE                  |                                                                      |
| BBC  | (4,C)  | 12,BBC                 |                                                                      |
| E    | (0,E)  | 13,E                   |                                                                      |
| DD   | (8,D)  | 14,DD                  |                                                                      |
| DA   | (8,A)  | 15,DA                  |                                                                      |
| EF   | (13,F) | 16,EF                  |                                                                      |
| F    | (0,F)  | 17,F                   |                                                                      |
|      |        |                        |                                                                      |
Wynik: 0A1A0B3B0C2A3C0D6A1E3E4C0E8D8A13F0F
Uwaga: nie musimy zapisywać słownika, podczas dekompresji odtwarzamy pierwotny słownik.

Kompresja stratna przykłady: JPEG, MP3, MP4



