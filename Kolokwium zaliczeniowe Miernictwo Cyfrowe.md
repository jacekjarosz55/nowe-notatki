**Błąd pomiaru** to różnica między wartością zmierzoną a wartością rzeczywistą wielkości mierzonej. Błędy pomiarowe mogą być systematyczne (spowodowane przez czynniki mające stały wpływ na wynik pomiaru) lub przypadkowe (wynikające z losowych fluktuacji w procesie pomiarowym).
 **Niepewność pomiaru** to parametr związany z wynikiem pomiaru, który charakteryzuje rozrzut wartości, które można rozsądnie przypisać wielkości mierzonej. Wyraża ona zaufanie do dokładności pomiaru i obejmuje wszelkie możliwe źródła błędów.


## Niepewność standardowa

**Niepewność standardowa** wyniku pomiaru $u$ jest miarą rozproszenia wartości pomiarowych wokół średniej wartości. Oblicza się ją za pomocą wzoru:
### a. dla próbki danych populacji 
$$u = \sqrt{\frac{\sum^{N}_{i=1}(x_i - \bar{x})^2}{N-1}}$$
gdzie:
- $N$ - liczba pomiarów,
- $x_i$ - poszczególne wyniki pomiarów,
- $\bar{x}$ - średnia arytmetyczna próbki

Dla uproszczenia:
$$ u = \sqrt{\frac{\delta_1^2 + \delta_2^2 + \dots + \delta_N^2}{N -1}}$$
Gdzie $\delta_{x}$ jest różnicą poszczególnego wyniku od średniej wszystkich wyników


### b. dla całej populacji
$$u = \sqrt{\frac{\sum^{N}_{i=1}(x_i - \micro)^2}{N}}$$
gdzie:
- $N$ - liczba pomiarów,
- $x_i$ - poszczególne wyniki pomiarów,
- $\micro$ - średnia arytmetyczna wyników pomiarów

## Prawo przenoszenia niepewności standardowych

Jeżeli mamy funkcję $z = f(x,y,\dots)$, to niepewność standardową $u(z)$ możemy obliczyć z niepewności standardowej poszczególnych zmiennych

$$ u(z) = \sqrt{
\left(\frac{\partial f}{\partial x}\cdot u(x)\right)^2 + \left(\frac{\partial f}{\partial y}\cdot u(y)\right)^2 + \dots

}$$ 
## Dyskretna transformata Fouriera

**Dyskretna transformata Fouriera** tworzy z ciągu próbek sygnału $a_n \in \mathbb{R}$ ciąg *harmonicznych* $A_n \in \mathbb{C}$: 
$$
A_k = \sum^{N-1}_{n=0}a_n\cdot e^{-i\frac{2\pi n k}{N}}$$
	Gdzie:
 - $k$ - indeks harmonicznej, $0 \le k \le N-1$,
 - $n$ - indeks próbki
 - $N$ - liczba próbek
 - $i$ - jednostka urojona
 
**Bardzo przydatne!** 
- $e^0 = 1$
- $\cos(-\alpha) = \cos(\alpha)$
- $\sin(-\alpha) = -\sin(\alpha)$
- $e^{i\alpha} = \cos\alpha + i \sin\alpha$, z czego wynika że:$e^{-i\alpha} = \cos(-\alpha) + i\sin(-\alpha) = \cos(\alpha) - i \sin(\alpha)$

$$ A_k = \sum^{N-1}_{n=0} \left[a_n \cdot \left( \cos\frac{2 \pi n k}{N} - i\sin\frac{2 \pi n k}{N}\right)\right]$$
## Przetworniki analogowo-cyfrowe; podstawowe rodzaje i zasady przetwarzania


https://pl.wikipedia.org/wiki/Przetwornik_analogowo-cyfrowy
Przetwornik analogowo-cyfrowy (ADC) przekształca sygnał analogowy na cyfrowy. Podstawowe rodzaje ADC obejmują:

- Przetworniki z sukcesywną aproksymacją (SAR),
- Przetworniki sigma-delta (ΔΣ),
- Przetworniki flash.

Zasady przetwarzania polegają na próbkowaniu sygnału analogowego z określoną częstotliwością i kwantyzacji wartości sygnału na dyskretne poziomy.

- Pełna skala pomiaru = od 0 do 10 woltów.
- Rozdzielczość przetwornika jest równa 12 bitów, czyli $2^{12} = 4096$ poziomów kwantyzacji.
- Rozdzielczość napięciowa wynosi: (10–0)/4096 = 0,00244 wolta = 2,44 mV.

### Rodzaje Przetworników ADC

1. **Przetworniki z Całkowaniem Dwubiegunowym (Integrating ADC)**
    
    - **Zasada działania:** Przetworniki te działają na zasadzie całkowania napięcia wejściowego przez określony czas, a następnie porównywania wyniku całkowania z napięciem referencyjnym.
    - **Zastosowania:** Doskonałe do pomiarów wolnozmiennych sygnałów, jak w aplikacjach przemysłowych i instrumentach pomiarowych.
2. **Przetworniki z Przetwarzaniem Próbkowania (Successive Approximation Register ADC - SAR ADC)**
    
    - **Zasada działania:** SAR ADC działają na zasadzie sukcesywnej aproksymacji, gdzie napięcie wejściowe jest porównywane z wartością generowaną przez wewnętrzny przetwornik DAC (Digital-to-Analog Converter), a wynik porównania jest używany do ustawienia kolejnych bitów wyniku.
    - **Zastosowania:** Powszechnie stosowane w szerokim zakresie aplikacji, w tym w systemach akwizycji danych i aplikacjach o średniej i wysokiej rozdzielczości.
3. **Przetworniki Sigma-Delta (ΣΔ ADC)**
    
    - **Zasada działania:** Sigma-Delta ADC działają na zasadzie modulacji gęstości impulsów (Pulse Density Modulation), gdzie sygnał analogowy jest przekształcany w ciąg impulsów o zmiennej gęstości, który jest następnie filtrowany i dekodowany na sygnał cyfrowy.
    - **Zastosowania:** Idealne do wysokorozdzielczych pomiarów sygnałów audio, precyzyjnych instrumentów pomiarowych i aplikacji wymagających niskiego szumu.
4. **Przetworniki Flash ADC**
    
    - **Zasada działania:** Flash ADC działają na zasadzie równoległego porównania napięcia wejściowego z szeregiem napięć referencyjnych za pomocą matrycy komparatorów, co pozwala na bardzo szybkie przetwarzanie sygnałów.
    - **Zastosowania:** Używane w aplikacjach wymagających bardzo szybkiego przetwarzania, takich jak oscyloskopy cyfrowe i systemy radarowe.
5. **Przetworniki z Ciągłym Czasem Przetwarzania (Continuous-Time ADC)**
    
    - **Zasada działania:** Te przetworniki nie przetwarzają sygnałów w określonych odstępach czasu, ale ciągle, co pozwala na uzyskanie bardzo niskiego opóźnienia.
    - **Zastosowania:** Używane w aplikacjach wymagających bardzo niskiego opóźnienia, takich jak systemy komunikacyjne.

### Zasady Przetwarzania Sygnałów przez ADC

1. **Próbkowanie (Sampling)**
    - Próbkowanie polega na pobieraniu wartości sygnału analogowego w określonych odstępach czasu. Częstotliwość próbkowania musi być co najmniej dwa razy większa od najwyższej częstotliwości sygnału (zgodnie z twierdzeniem Nyquista), aby uniknąć aliasingu.
2. **Kwantyzacja (Quantization)**
    - Kwantyzacja to proces przypisywania próbkowanym wartościom sygnału analogowego najbliższych dostępnych wartości cyfrowych. Wiąże się to z pewnym błędem kwantyzacji, który zależy od rozdzielczości przetwornika.
3. **Kodowanie (Encoding)**
    - Kodowanie to przypisywanie cyfrowych wartości binarnych do skwantyzowanych wartości sygnału. Ilość bitów użytych do kodowania określa rozdzielczość przetwornika i jego dokładność.



Amplituda: wysokość fali
Międzyszczytowa: między wartością maksymalną i minimalną, dla sinusoidy to dwukrotność amplitudy
Wzmocnienie: proporcja między sygnałem wyjściowym a wejściowym
Decybel:  20 log x


## Zadania 

Niepewność standardowa (jak mamy $\Delta(x_1)$, $\Delta(x_2)$ ):
(przykład dla funkcji $y = x_1 + x_2$, dla $y = x_1 - x_2$ po prostu odejmujemy zamiast odjąć deltę)
- $$u_s(y) = us(x_1 + x_2) = \frac{\Delta ap(x)}{\sqrt3} = \frac{\Delta(x_1) + \Delta(x_2)}{\sqrt3}$$
- $$u_s(y) = us(x_1 - x_2) = \frac{\Delta ap(x)}{\sqrt3} = \frac{\Delta(x_1) - \Delta(x_2)}{\sqrt3}$$


Transformata fouriera: 
	kąt = potęga e /  i
- składowa stała $U_0$:  to co jest współczynnikiem $e^x$
$$ U_0 = U(0) / J
- amplituda: $$U_m = U_k \cdot \sqrt{2}$$ 
- prawdziwa wartość częstotliwośći harmonicznej $f_k$: $$f_k = \frac{k\cdot f_z}{N}$$


Podwójne całkowanie:
$$ U_x = \frac {N_2}{f_w} \cdot \frac {U_\text{ref}}{T_1}  $$
gdzie: 
- $U_x$ - napięcie zmierzone
- $f_w$ - częstotliwość impulsów
- $U_\text{ref}$ - napięcie referencyjne
- $T_1$ - czas pierwszego całkowania
- $N_2$ - ilość próbek drugiego całkowania



niepewność aparaturowa:
Po prostu liczysz to co masz napisane przez producenta

Względny błąd zliczania $\delta(N)$:
Dla czasu pomiaru $T_p$ i częstotliwości $f_x$, $N$ - ilość próbek:
$$\delta(N) = \frac{\Delta(N)}{N} = \frac {1}{N} = \frac{1}{T_p \cdot f_x}$$

