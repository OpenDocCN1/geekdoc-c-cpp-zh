# 150 Applied Time Series Analysis with R

(a)

![](bbox=[0.168, 0.135, 0.843, 0.243])

(b)

![](bbox=[0.168, 0.275, 0.843, 0.383])

(c)

![](bbox=[0.168, 0.415, 0.843, 0.523])

(d)

![](bbox=[0.168, 0.555, 0.843, 0.663])

FIGURE 3.27
Sunspot data from 1749–2008 and the first three additive components associated with the AR(9) fit in Example 3.15 whose factor table is designed in Table 3.5. (a) Realization. (b) Component
1: f=0.09. (c) Component 2: f=0. (d) Component 3: f=0.19.

due to the characteristic equation on the unit circle. One modification of ARMA(p,q) is designed to take into account seasonal behavior in data. For example, quarterly data (e.g., breaking the year into 4 month groups) will have seasonal characteristics implying that there is a natural correlation structure between, $X_i$ and $X_{i-4}$, is, between the current quarter and the quarter last year. In this case, it makes sense to include factors in the model as $\phi(B^4)=1-\phi_1B^4-\phi_2B^8-\dots-\phi_4B^{16}$, that take into account this four-quarter year relationship. For example, we might have that $\phi(B^4)=1-0.9B^4$ or $\phi(B^4)=1-B^4+0.8B^4$, is, the models $X_i=X_{i-4}+a_i$