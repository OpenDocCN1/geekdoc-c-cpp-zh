(3.68) 
$$ \sum_{k \in \mathbb{Z}} N_1(t+k) \equiv 1. $$

# Second-order B-spline

(3.69) 
$$ N_2(t) = N_1(t) * N_1(t) $$

(3.70) 
$$ = \begin{cases} t & t \in [0, 1] \\ 2-t & t \in [1, 2] \\ 0 & \text{otherwise.} \end{cases} $$

From the convolution property, we have

(3.71) 
$$ \hat{N}_2(\omega) = \left( \hat{N}_1(\omega) \right)^2 $$

(3.72) 
$$ \hat{N}_1(\omega) = \left( \frac{1 - e^{-j\omega}}{j\omega} \right)^2. $$

Again, we find here that

(3.73) 
$$ \hat{N}_2(0) = 1; $$

(3.74) 
$$ \hat{N}_2(2\pi k) = 0; \quad k \in \mathbb{Z} \setminus \{0\}. $$

Consequently, \(N_2(t)\) also satisfies the conditions for partition of unity. In fact, from the recursive relation of \(B\)-spline