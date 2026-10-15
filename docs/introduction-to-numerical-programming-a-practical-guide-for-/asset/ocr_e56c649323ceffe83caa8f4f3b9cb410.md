The most important and widely used variant is the fourth-order Runge–Kutta method ($p = 4$), which offers both a good control of the local truncation error and an easily implementable functional form. Following the same reasoning for determining the coefficients $\alpha_i$, $\beta_{ij}$, and $w_i$ as in the case $p = 2$, there results a nonlinear system of 10 equations with 13 unknowns, which, being underdetermined, does not have a unique solution. Several sets of coefficients are in use, being though preferred those either featuring simplicity or favoring efficient storage usage. The commonly employed variant of the fourth-order Runge–Kutta method is defined by the relations:

$y_{m+1} = y_m + \frac{1}{6}\left(k_1 + 2k_2 + 2k_3 + k_5\right) + O(h^5), \tag{12.34}$
$
\begin{cases}
k_1 = h f(t_m, y_m),\\
k_2 = h f(t_m + h/2, y_m + k_1/2),\\
k_3 = h f(t_m + h/2, y_m + k_2/2),\\
k_4 = h f(t_m + h, y_m + k_3),
\end{cases} \tag{12.35}$

and it implies at each propagation step four evaluations of the right-hand-side function $f(t,y)$. The corresponding truncation error reflects the neglect of the $O(h^5)$ terms:

$\Delta_{m+1} \sim K h^5. \tag{12.36}$

It is noteworthy that, for a right-hand-side function $f$ independent of $y$, the differential equation turns into the simple integral of $f$ over the interval $[t_m, t_m + h]$, and the fourth-order Runge–Kutta method becomes equivalent with Simpson’s rule (see Chapter 10):

$y_{m+1} = y_m + \frac{h}{6}\left[f(t_m) + 4f(t_m + h/2) + f(t_m + h)\right].$

The double values of the standard coefficients of Simpson’s rule $(1/3, 4/3, 1/3)$ stem from the definition of the integration interval length as $2h$ instead of $h.$

In addition to the satisfactory precision and the simple implementation, being an explicit one-step algorithm, the fourth-order Runge–Kutta method stands out by its self-starting ability, as well. The Runge–Kutta solver is also useful for providing initial values for more accurate, yet not self-starting multistep methods.

Taking advantage of the simple structure of the coefficients $k_1$, $k_2$, $k_3$, and $k_4$ of the fourth-order Runge–Kutta method 12.34–12.35, for a system of $n$ first-order ODEs, it is convenient to explicitly refer to the values of the right-hand-side functions $f_i$:

$y_{m+1,i} = y_{m,i} + \frac{h}{6}\left(f_{1,i} + 2f_{2,i} + 2f_{3,i} + f_{4,i}\right), \quad i = 1,2,\dots,n, \tag{12.37}$
$
\begin{cases}
f_{1,i} = f_i(t_m, \{y_{m,i}\}),\\
f_{2,i} = f_i(t_m + h/2, \{y_{m,i} + (h/2)f_{1,i}\}),\\
f_{3,i} = f_i(t_m + h/2, \{y_{m,i} + (h/2)f_{2,i}\}),\\
f_{4,i} = f_i(t_m + h, \{y_{m,i} + h f_{3,i}\}).
\end{cases} \tag{12.38}$

The curly braces indicate the whole set of arguments for all solution components (running over all values of $i$). Obviously, the formalism can also be applied for solving Cauchy problems for higher-order ODEs, by first transforming the equation into a system of first-order ODEs.

The routine RungeKutta (Listing 12.3) represents the one-to-one coding of the described algorithm for solving an “elementary” Cauchy problem for a system of first-order ODEs. Concretely, the routine performs on each call a one-step propagation of the known solution $(y_{m,i}, i = 1,2,\dots n)$ from $t_m$ to $t_{m+1} = t_m + h$, producing updated components $y_{m+1,i}$ according to Equations 12.37 through