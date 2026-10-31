This problem is further determined by the following boundary conditions as described before:

$T(r,t)=\begin{cases}T_0=\text{const.}&\text{if }r\le r_c\\0&\text{if }r>r_i\end{cases}$

Additionally, the following initial conditions hold assuming that the insulator was uniformly cooled to 0 at $t=0$:

$T(r,0)=\begin{cases}T_0=\text{const.}&\text{if }r\le r_c\\0&\text{else}\end{cases}\quad(6.55)$

In order to devise an analog computer program to solve (6.54) the insulator with thickness $r_i-r_c$ will be subdivided into $n\in\mathbb N$ slices of equal thickness $\Delta r$. Thus, the $T(r,t)$ are replaced by a finite number of $T_i(t)$ by approximating the differentials by differential quotients with respect to $r$ yielding a number of coupled ordinary differential equations which can then be readily solved by an analog computer. This is based on the following approximations for first and second derivatives

$\left.\frac{\partial f(x,t)}{\partial x}\right|_{x_i}\approx\frac{f_{i+1}(t)-f_{i-1}(t)}{2\Delta x}\quad\text{and}\quad(6.56)$
$\left.\frac{\partial^2 f(x,t)}{\partial x^2}\right|_{x_i}\approx\frac{f_{i+1}(t)-2f_i(t)+f_{i-1}(t)}{(\Delta x)^2}.\quad(6.57)$

Applying (6.56) and (6.57) to (6.54) yields the following general expression

$\dot T_i = a\left(\frac{T_{i+1}-2T_i+T_{i-1}}{(\Delta r)^2}+\frac{1}{r_c+i\Delta r}\frac{T_{i+1}-T_{i-1}}{2\Delta r}\right).\quad(6.58)$
which can be readily implemented on an analog computer since it only contains a derivative with respect to $t$.

In the following example the insulator will be divided into four equally wide slices and it will be assumed that $r_i=5r_c$ yielding $\Delta r=\frac{r_i-r_c}{4}=r_c$. Accordingly, (6.58) can be rewritten as follows:
$\dot T_i = a\left(\frac{T_{i+1}-2T_i+T_{i-1}}{(\Delta r)^2}+\frac{T_{i+1}-T_{i-1}}{2(i+1)(\Delta r)^2}\right)$
$=\frac{a}{(\Delta r)^2}\left(T_{i+1}-2T_i+T_{i-1}+\frac{1}{2(i+1)}(T_{i+1}-T_{i-1})\right)$