
Projekt mikroprocesora oraz układów towarzyszących
Wymagania:
Adresowanie 4096 słów pamięci operacyjnej
Wspierane adresowania: domyślne, natychmiastowe, bazowe z przemieszczeniem
Segmentacja pamięci: podział na segment kodu programu i segment danych
Rejestry segmentowe: CS, DS, SS (16-bitowe)
Rejestr licznika rozkazów: tylko do odczytu
8 rejestrów uniwersalnych: R0-R7
Obsługa stosu
Obsługiwane rozkazy:
Przesyłanie danych rej-nat, rej-rej, rej-pam
Dodawanie/odejmowanie rej-nat, rej-pam
Mnożenie rej-nat, rej-pam
Porównywanie rej-nat, rej-pam
Wywołanie podprogramu
Skoki bezwarunkowe i warunkowe (gdy większe, mniejsze, równe)
Rozkazy Mikroprocesora
1. Przesyłanie danych:
MOV R L: Przesłanie wartości natychmiastowej do rejestru

Kod instrukcji: 0000
Format: |0000|0|aaaa|----|llllllll|
Przykład: MOV R0, 5 → 0000 0 0000 ---- 00000101
MOV R R: Przesłanie wartości z rejestru do rejestru

Kod instrukcji: 0000
Format: |0000|0|aaaa|bbbb|--------|
Przykład: MOV R1, R2 → 0000 0 0001 0010 --------
MOV R BX: Przesłanie wartości z pamięci (adres bazowy i przemieszczenie) do rejestru

Kod instrukcji: 0000
Format: |0000|1|aaaa|---|--------|
Przykład: MOV R3, [BX] → 0000 1 0011 --- --------
2. Operacje Arytmetyczne:
ADD R L: Dodanie wartości natychmiastowej do rejestru

Kod instrukcji: 0001
Format: |0001|0|aaaa|---|llllllll|
Przykład: ADD R4, 10 → 0001 0 0100 --- 00001010
SUB R L: Odejście wartości natychmiastowej od rejestru

Kod instrukcji: 0010
Format: |0010|0|aaaa|---|llllllll|
Przykład: SUB R5, 3 → 0010 0 0101 --- 00000011
MUL R L: Mnożenie rejestru przez wartość natychmiastową

Kod instrukcji: 0011
Format: |0011|0|aaaa|---|llllllll|
Przykład: MUL R6, 2 → 0011 0 0110 --- 00000010
3. Porównania:
CMP R L: Porównanie rejestru z wartością natychmiastową
Kod instrukcji: 0100
Format: |0100|0|aaaa|---|llllllll|
Przykład: CMP R7, 5 → 0100 0 0111 --- 00000101
4. Podprogramy:
CALL ADR: Wywołanie podprogramu, zapisuje adres powrotny na stosie

Kod instrukcji: 0110
Format: |0110|0|----|---|llllllll|
Przykład: CALL 100 → 0110 0 ---- --- 01100100
RET: Powrót z podprogramu, pobiera adres powrotny ze stosu

Kod instrukcji: 0111
Format: |0111|0|----|---|--------|
Przykład: RET → 0111 0 ---- --- --------
5. Stos:
PUSH R: Umieszczenie wartości rejestru na stosie

Kod instrukcji: 1000
Format: |1000|0|aaaa|---|--------|
Przykład: PUSH R0 → 1000 0 0000 --- --------
POP R: Pobiera wartość ze stosu do rejestru

Kod instrukcji: 1001
Format: |1001|0|aaaa|---|--------|
Przykład: POP R1 → 1001 0 0001 --- --------
6. Skoki:
JMP ADR: Skok bezwarunkowy do adresu

Kod instrukcji: 1010
Format: |1010|0|----|---|llllllll|
Przykład: JMP 200 → 1010 0 ---- --- 11001000
JE ADR: Skok warunkowy, jeśli równy

Kod instrukcji: 1011
Format: |1011|0|----|---|llllllll|
Przykład: JE 150 → 1011 0 ---- --- 10010110
JG ADR: Skok warunkowy, jeśli większy

Kod instrukcji: 1100
Format: |1100|0|----|---|llllllll|
Przykład: JG 175 → 1100 0 ---- --- 10101111
JL ADR: Skok warunkowy, jeśli mniejszy

Kod instrukcji: 1101
Format: |1101|0|----|---|llllllll|
Przykład: JL 125 → 1101 0 ---- --- 01111101
Program Demonstracyjny
Poniżej przedstawiono przykładowy program, który demonstruje możliwości mikroprocesora. Program jest zapisany w pseudokodzie oraz assemblerze.

Pseudokod:
Załaduj wartość 5 do rejestru R0
Załaduj wartość 10 do rejestru R1
Dodaj wartość 3 do rejestru R0
Porównaj wartość rejestru R0 z wartością rejestru R1
Jeśli R0 jest mniejsze niż R1, skocz do etykiety LESS
Jeśli R0 jest równe R1, skocz do etykiety EQUAL
Skocz do etykiety GREATER
LESS: Umieść wartość rejestru R0 na stosie, zakończ program
EQUAL: Umieść wartość rejestru R1 na stosie, zakończ program
GREATER: Umieść wartość rejestru R1 na stosie, zakończ program



| Rozkaz  | kkkk | d   | aaa        | bbb | llllllll          | Instrukcja |     |                                                                                   |
| ------- | ---- | --- | ---------- | --- | ----------------- | ---------- | --- | --------------------------------------------------------------------------------- |
| MOV R L | 0000 | 0   | $a_1 a_2 $ | --- | $l_1 l_2 l_3 l_4$ | --         | $$  | przesłanie wartości<br>natychmiastowej do rejestru,                               |
|         |      |     |            |     |                   |            |     | przesłanie wartości z rejestru<br>do rejestru,                                    |
|         |      |     |            |     |                   |            |     | przesłanie wartości z<br>pamięci do rejestru,                                     |
|         |      |     |            |     |                   |            |     | przesłanie wartości z<br>pamięci (adres bazowy i<br>przemieszczenie) do rejestru, |
|         |      |     |            |     |                   |            |     | dodanie wartości<br>natychmiastowej do rejestru                                   |
|         |      |     |            |     |                   |            |     | dodanie wartości z pamięci<br>do rejestru,                                        |
|         |      |     |            |     |                   |            |     | odejmowanie wartości<br>natychmiastowej od rejestru,                              |
|         |      |     |            |     |                   |            |     | odejmowanie wartości z<br>pamięci od rejestru,                                    |
|         |      |     |            |     |                   |            |     | mnożenie rejestru przez<br>wartość natychmiastową,                                |
|         |      |     |            |     |                   |            |     | mnożenie rejestru przez<br>pamięć,                                                |
|         |      |     |            |     |                   |            |     | porównanie rejestru z<br>wartością natychmiastową,                                |
|         |      |     |            |     |                   |            |     | porównanie rejestru z<br>pamięcią,                                                |
|         |      |     |            |     |                   |            |     | wywołanie podprogramu,<br>zapisuje adres powrotny na<br>stosie,                   |
|         |      |     |            |     |                   |            |     | powrót z podprogramu,<br>pobiera adres powrotny ze<br>stosu,                      |
|         |      |     |            |     |                   |            |     | pobiera wartość ze stosu do<br>rejestru,                                          |
|         |      |     |            |     |                   |            |     | skok bezwarunkowy do<br>adresu,                                                   |
|         |      |     |            |     |                   |            |     | skok warunkowy, jeśli równy,                                                      |
|         |      |     |            |     |                   |            |     | skok warunkowy, jeśli<br>większy,                                                 |
|         |      |     |            |     |                   |            |     | skok warunkowy, jeśli<br>mniejszy,                                                |
