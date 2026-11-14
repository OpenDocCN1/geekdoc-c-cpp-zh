The next case is \(s < 0 < x\). Noting that, in that case,

\(g(x) - g(s) = p(s - x) + (h + p)E(x - D(L))^+,\)

it is easy to check that the formula giving \(\psi_s(x)\) is the formula (14.9.1) with an additional term

\(\frac{h+p}{\lambda} \sum_{j=0}^{[x]} E(x - j - D(L))^+.\)

This term is equal to

\(\frac{h+p}{\lambda} \exp - \lambda L \sum_{j=0}^{[x]} \frac{(\lambda L)^j}{j!} \left(x - \frac{1}{2}[x] - \frac{1}{2}j\right)([x] - j + 1).\)

Collecting results we obtain, for \(s < 0 < x\)

(14.9.2) \(\psi_s(x) = -pL(x - s) + \frac{1}{2}\lambda L^2 p + \\ + \frac{h}{\lambda} \exp - \lambda L \sum_{j=0}^{[x]} \frac{(\lambda L)^j}{j!} \left(x - \frac{1}{2}[x] - \frac{1}{2}j\right)([x] - j + 1) \\ - \frac{p}{\lambda} \exp - \lambda L \sum_{j=s+[x]+1}^{[x] - s} \frac{(\lambda L)^j}{j!} \left(x - \frac{1}{2}[x] - \frac{1}{2}j\right)([x] - j + 1) \\ + \frac{p}{\lambda} \exp - \lambda L \sum_{j=0}^{[x] - s} \frac{(\lambda L)^j}{j!} \left((x - j)s + \frac{s}{2} - \frac{s^2}{2}\right).\)

Consider now the case \(0 < s\). We recall that

\(g(x) - g(s) = p(s - x) + (h + p)E(x - D(L))^+ - (s - D(L))^+].\)

Again we have to add to the expression (14.9.1) an additional term given by

\(\frac{h+p}{\lambda} \sum_{j=0}^{[x] - s} E([(x - j - D(L))^+ - (s - D(L))^+] \\ + \exp - \lambda L \left[ \sum_{j=[x] - s + 1}^{\infty} E[(x - j - D(L))^+ - (s - D(L))^+] \sum_{k=j+1}^{\infty} \frac{(\lambda L)^k}{k!} \right]\)

We can express the additional term multiplying \(\frac{h+p}{\lambda}\) as follows

\(\exp - \lambda L \sum_{j=0}^{[x] - s - x} (x - j - s) \frac{(\lambda L)^k}{k!} + \exp - \lambda L \sum_{j=0}^{[x] - s - x} (x - j - k) \frac{(\lambda L)^k}{k!} \\ + \exp - 2\lambda L \lfloor_{j=[x] - s + 1}^{[x]} \sum_{m=0}^{k-j} \left( \sum_{m=0}^{[x] - j - s} (x - j - s) \frac{(\lambda L)^m}{m!} - \sum_{m=[x] - j + 1}^{s} (s - m) \frac{(\lambda L)^m}{m!} \right) \\ \cdot \sum_{k=j+1}^{\infty} \frac{(\lambda L)^k}{k!} \rfloor - \exp - 2\lambda L \sum_{j=[x] + 1}^{\infty} \sum_{m=0}^{\infty} (s - m) \frac{(\lambda L)^m}{m!} \sum_{k=j+1}^{\infty} \frac{(\lambda L)^k}{k!}\)