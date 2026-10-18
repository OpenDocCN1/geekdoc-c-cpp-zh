\(\bar{\phi}=\frac{\sqrt{5}-1}{2}\). So,

$$G^2(z)=\frac{1}{5}\left[(1-\phi z)^{-2}+(1-\bar{\phi}z)^{-2}-2(1-\phi z)^{-1}(1-\bar{\phi}z)^{-1}\right].$$

Hence, the coefficient of \(z^{n+3}\) in \(G^2(z)\) is:

$$\frac{1}{5}\left[(n+4)\phi^{n+3}+(n+4)\bar{\phi}^{n+3}-2(\phi^{n+3}\bar{\phi}^{0}+\phi^{n+2}\bar{\phi}+\cdots+\phi^1\bar{\phi}^{n+2}+\phi^0\bar{\phi}^{n+3})\right].$$

Let \(S=\phi^{n+3}+\phi^{n+2}\bar{\phi}+\cdots+\phi\bar{\phi}^{n+2}+\bar{\phi}^{n+3}\). So, \(S[1-\frac{\bar{\phi}}{\phi}]=\phi^{n+3}-\frac{\bar{\phi}^{n+4}}{\phi}=\frac{\phi^{n+4}-\bar{\phi}^{n+4}}{\phi}\).

Hence, \(S=\phi^{n+4}-\bar{\phi}^{n+4}\), as \(\phi-\bar{\phi}=1\). Therefore,

$$\nu_0=\frac{1}{5}\left[(n+4)(\phi^{n+3}+\bar{\phi}^{n+3})-2(\phi^{n+4}-\bar{\phi}^{n+4})\right]. \tag{8.52}$$

Putting the values of \(\phi\) and \(\bar{\phi}\) in the above expression of \(\nu_0\), we get the number of 0’s in all \(n\)-bit valid codewords. The number of 1’s in all \(n\)-bit valid codewords is given by

$$\nu_1=nF_{n+2}-\nu_0. \tag{8.53}$$

For large \(n\), \(\nu_0\approx\frac{(n+4-2\phi)\phi^{n+3}}{5}=\frac{(n+0.764)\phi^{n+3}}{5}\). The ratio of \(\nu_0\) to the total number of bits \(nF_{n+2}\) asymptotically tends to \(\frac{\phi}{\sqrt{5}}=72.36\%\). Such a large asymmetry in the number of 0’s and 1’s can be exploited in applications involving low energy wireless communication by keeping the transmitter silent or off during the dominant symbols (0’s in this case), thereby reducing the average power of signal transmission.

On the other hand, corresponding to \(m\)-bit binary representation of numbers, we need \(n\) bits in FNS where \(n\) is the least integer satisfying the inequality \(F_{n+2}-1>2^m-1\). Noting that \(F_{n+2}\approx\frac{\phi^{n+2}}{\sqrt{5}}\) for large \(n\), \(\frac{\phi^{n+2}}{\sqrt{5}}>2^m\), i.e., \(n\approx\left\lceil\frac{m+\log\sqrt{5}}{\log\phi}\right\rceil-2\). For \(m=8,16,32,64,128,256,512\) and 1024, the corresponding values of \(n\) are 12,