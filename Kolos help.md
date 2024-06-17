## Niepewności standardowe

1. dla $y_a = x_1 + x_2$: $$u_s(y_a) = u_s(x_1 + x_2) = \frac{\Delta ap(y_a)}{\sqrt3}$$ gdzie $\Delta ap(Y_a) = \Delta(x_1) + \Delta(x_2)$

2. dla $y_b = x_1 - x_2$: $$u_s(y_a) = u_s(x_1 - x_2) = \frac{\Delta ap(y_b)}{\sqrt3}$$ gdzie $\Delta ap(Y_b) = \Delta(x_1) - \Delta(x_2)$

## Fourier

1. Prawdziwa wartość napięcia $U_0$: $$\frac{U_0}{N}$$ $U_0$ to to co jest przy $e$ (np. dla $5e^{-j0\degree}$ jest to $5$)

2.  Amplituda $U_m$: $$\frac{U_k}{N}$$$U_K$ to to co jest przy $e$ (jak wyżej)

3. Kąt fazowy $\phi$:  to co jest przy $j$ w wykładniku $e$ np(dla $41e^{-j30\degree}$ jest to $-30\degree$)
4. Prawdziwa wartość częstotliwości harmonicznej o indeksie $k$ dla częstotliwości próbkowania $f_s$: $$f_k = \frac{k \cdot f_s}{N}$$
## Podwójne całkowanie

1. Wartość napięcia $U_x$ dla:
	-  $N_2$ próbek drugiego całkowania
	-  $f_w$ częstotliwość impulsów
	-  $U_\text{ref}$ napięcie referencyjne 
	-  $T_1$ czas pierwszego całkowania
	$$U_x = \frac{N_2}{f_w} \cdot \frac{U_\text{ref}}{T_1}$$
2. Niepewność aparaturowa pomiaru napięcia
   (wystarczy policzyć to co jest napisane tekstem) (zakres pomiarowy  = $U_\text{ref}$): $$ \Delta(U_x) =  a\%\text{wartości mierzonej} + b\%\text{zakresu pomiarowego}$$
## Empiryczne odchylenie / bezwzględna niepewność

Mamy:
- $N$ - liczba pomiarów
- $U_N$ zakres
- $S_U$ - empiryczne  odchylenie standardowe średniej
- $u_{ap}(U)$ - bezwzględna standardowa niepewność aparaturowa (podana)
- $u_s(U) = ?$ - bezwzględna niepewność standardowa 
$$U_s(U) = \sqrt{{s_U}^2 + {u_{ap}}^2}$$


