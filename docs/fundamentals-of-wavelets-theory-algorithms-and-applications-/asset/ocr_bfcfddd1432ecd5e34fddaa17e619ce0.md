(10.57)
\(\begin{cases} t_{-m+1}^s = t_{-m+2}^s = \cdots = t_0^s = 0, \\ t_k^s = k2^{-s}, k = 1, \dots, 2^s - 1, \\ t_{2^s}^s = t_{2^s+1}^s = \cdots = t_{2^s+m-1}^s = 0. \end{cases}\)

For the knot sequence (10.57) we define the \(B\)-spline (\(m \ge 2\)) as [36]

(10.58)
\(B_{m,k,s}(x) := (t_{k+m}^s - t_k^s) \times [t_k^s, t_{k+1}^s, \dots, t_{k+m}^s] (t-x)_+^{m-1},\)

where \([t_k^s, \dots, t_{k+m}^s]_t\), is the \(m\)th order divided difference of \((t-x)_+^{m-1}\) with respect to \(t\) and \((x)_+ := \max(0, x)\). Wavelets can be obtained from the corresponding spline scaling functions. Instead of going into the details of construction of scaling functions and wavelets on bounded interval, we provide their explicit formulas in Section 10.9. Interested readers may find details in [23, 32, 33].

The support of the inner (without multiple knots) \(B\)-spline occupies \(m\) segments and that of the corresponding s.o. wavelet occupies \(2m - 1\) segments. At any scale \(s\) the discretization step is \(1/2^s\) which, for \(s > 0\), gives \(2^s\) number of segments in \([0, 1]\). Therefore, to have at least one inner wavelet, the following condition must be satisfied:

(10.59)
\(2^s \ge 2m - 1.\)