If \(\bar{S}\) is the complex conjugate of \(S\), then

\(\begin{aligned} \bar{S}\bar{S} &= \sum_{j=0}^{n-1} f(\text{TR}_k(\delta^j \zeta^{-k^j})) + \sum_{j \neq k} f(\text{TR}_k(\delta^j \zeta^{-k^j})) \\ &= 2^r - 1 + \sum_{a \in R^+} f(\text{TR}_k(a)) - \sum_{j=0}^{n-1} f(\text{TR}_k(\delta^{2k} \zeta^{-k^j})) - \sum_{j=0}^{n-1} f(\text{TR}_k(-\zeta^{k^j})) \\ &= 2^r - 1 + \sum_{a \in R^+} f(\text{TR}_k(a)) - S - \bar{S} \end{aligned}\)

by Lemma 17.2.5. But \(\sum_{a \in R^+} f(\text{TR}_k(a)) = \sum_{a \in R} f(\text{TR}_k(a)) - \sum_{a \in 2R} f(\text{TR}_k(a)) = 0 - 0 = 0\) by Exercise 756. Rearranging gives \((S + \bar{S})(1) = 2^r\) and therefore

\((n_0 - n_2 + 1)^2 + (n_1 - n_3)^2 = 2^r\) (12.26)

by (12.25). Thus we need integer solutions to the equation \(x^2 + y^2 = 2^r\). By Exercise 757, the solutions are \(x = \delta_1 2^{(r-1)/2}\), and \(y = \delta_2 2^{(r-1)/2}\), where \(\delta_1\) and \(\delta_2\) are \(\pm 1\). By (12.26),

\(n_0 - n_2 = -1 + \delta_1 2^{(r-1)/2} \quad \text{and}\) (12.27)

\(n_1 - n_3 = \delta_2 2^{(r-1)/2}.\) (12.28)

However, \(2\mathbf{v}_k = \mathbf{v}_{2k}\) is a vector from Case II, which means that

\(n_0 + n_2 = 2^{r-1} - 1 \quad \text{and}\) (12.29)

\(n_1 + n_3 = 2^{r-1}.\) (12.30)

Solving (12.27), (12.28), (12.29), and (12.30) produces

\(n_0 = 2^{r-2} + \delta_1 2^{(r-3)/2} - 1, n_1 = 2^{r-2} + \delta_2 2^{(r-3)/2},\) (12.31)

\(n_2 = 2^{r-2} - \delta_1 2^{(r-3)/2}, \quad \text{and} \quad n_3 = 2^{r-2} - \delta_2 2^{(r-3)/2}.\) (12.32)

We can easily obtain \(n_j((0, \mathbf{v}_k) + \epsilon \mathbf{l}_{k+1})\) in terms of \(n_j = n_j(\mathbf{v}_k)\) as the following table shows:

| \\epsilon \\backslash j | 0 | 1 | 2 | 3 | Lee weight |
|---|---|---|---|---|---|
| 0 | \(n_0 + 1\) | \(n_1\) | \(n_2\) | \(n_3\) | \(2^r - \delta_2 2^{(r-1)/2}\) |
| 1 | \(n_3\) | \(n_0 + 1\) | \(n_1\) | \(n_2\) | \(2^r + \delta_2 2^{(r-1)/2}\) |
| 2 | \(n_2\) | \(n_3\) | \(n_0 + 1\) | \(n_1\) | \(2^r + \delta_2 2^{(r-1)/2}\) |
| 3 | \(n_1\) | \(n_2\) | \(n_3\) | \(n_0 + 1\) | \(2^r - \delta_2 2^{(r-1)/2}\) |

The column “Lee weight” is obtained from the equation \(w_{tL}((0, \mathbf{v}_k) + \epsilon \mathbf{l}_{k+1}) = n_1((0, \mathbf{v}_k) + \epsilon \mathbf{l}_{k+1}) + 2n_2((0, \mathbf{v}_k) + \epsilon \mathbf{l}_{k+1}) + n_3((0, \mathbf{v}_k) + \epsilon \mathbf{l}_{k+1})\) by using (12.31) and (12.32). Thus two of the four codewords have Lee weight \(2^{-(r-1)/2}\), while the other two have Lee weight \(2^r + 2^{(r-1)/2}\). Therefore Case III contributes \(2(4^r - 2^r) = 2^{r+1}(2^r - 1)\)

4 This is the only place in this proof where we require \(r\) to be odd.