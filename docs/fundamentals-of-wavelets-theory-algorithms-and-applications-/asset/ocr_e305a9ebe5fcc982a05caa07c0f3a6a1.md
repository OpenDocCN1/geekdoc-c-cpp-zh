6. \( N_m(t) \) is symmetric with respect to the center \( t^* = m/2 \):

\( N_m\left(\frac{m}{2} + t\right) = N_m\left(\frac{m}{2} - t\right) ; \quad t \in \mathbb{R} \)

(5.44)

7. \( N_m(t) \) behaves as a lowpass filter [ \( \hat{N}_m(0) = 1 \) ; see Figure 5.7].

8. \( N_m(t) \) has \( m \)th order of approximation in the sense that \( \hat{N}_m(\omega) \) satisfies the Strang-Fix condition

(5.45)

\(\begin{cases} \hat{N}_m(0) = 1, \text{ and} \\ D^j \hat{N}_m(2\pi k) = 0, \quad k \in \mathbb{Z} \\setminus \{0\} \quad \text{and} \quad j = 1, ..., m-1, \end{cases}\)

where \( D^j \) denotes the \( j^{\text{th}} \) order derivative. Consequently, \( N_m(t) \) locally reproduces all polynomials of order \( m \) [8, pp. 114–121].

9. \( N_m(t - k) \equiv 1 \) ; for all \( t \). This property is referred to as the *partition of unity* property.

10. *Total positivity*: \( N_m(t) \ge 0 \), for \( t \in [0, m] \). By virtue of the total positivity [6, p. 7] property of \( B \)-splines, coefficients of a \( B \)-spline series follow the shape of the data. For instance, if \( g(t) = \sum_j \alpha_j N_m(t - j) \), then

\( \alpha_j \ge 0 \quad \forall j \Rightarrow g(t) \ge 0 \)