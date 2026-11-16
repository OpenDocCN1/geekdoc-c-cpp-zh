+   (a) For each \( a \in \mathbb{Z}_4 \), there are exactly \( 4^{r-1} \) elements of \( \mathcal{R} \) with relative trace equal to \( a \).
+   (b) For each \( s \in \{0, 2\xi, 2\xi^2, \dots, 2\xi^{k-1}\} = 2\mathcal{R} \), \( \text{Tr}_r(s) \in \{0, 2\} \) with at least one value equaling 2.
+   (c) For \( a = 0 \) or 2, there are exactly \( 2^{r-1} \) elements of \( 2\mathcal{R} \) with relative trace equal to \( a \).

Before we give the Lee weight distribution of \( \widehat{\mathcal{K}}(r+1) \) we need one more computational result.

**Lemma 12.7.5** Let \( \mathcal{R} = \text{GR}(4^r) \) have primitive element \( \xi \). Let \( n = 2^r - 1 \). Suppose that \( \lambda \in \mathcal{R} \) but \( \lambda \notin 2\mathcal{R} \). Then all the elements of \( \mathcal{S} = \mathcal{S}_1 \cup \mathcal{S}_2 \), where \( \mathcal{S}_1 = \{(\xi^j - \xi^k) \mid 0 \le j \le n-1, 0 \le k \le n-1, j \neq k\} \) and \( \mathcal{S}_2 = \{\pm \lambda \xi^j \mid 0 \le j \le n-1\} \) are distinct, and they are precisely the elements of \( \mathcal{R} \setminus 2\mathcal{R} \).

**Proof:** By Exercise 748 the set of invertible elements in \( \mathcal{R} \) is \( \mathcal{R} \setminus 2\mathcal{R} \). We only need to show that the elements of \( \mathcal{S} \) are invertible and distinct because \( \mathcal{R} \setminus 2\mathcal{R} \) has \( 4^r - 2^r \) elements and, if the elements of \( \mathcal{S} \) are distinct, \( \mathcal{S} \) has \( (2^r - 1)(2^r - 2) + 2(2^r - 1) = 4^r - 2^r \) elements.

Since \( \lambda \) is invertible, the elements of \( \mathcal{S}_2 \) are invertible. Clearly, the elements of \( \mathcal{S}_2 \) are distinct as \( -\xi^j = \xi^j + 2\xi^j \) cannot equal \( \xi^k \) for any \( j \) and \( k \).

To show the elements of \( \mathcal{S}_1 \) are invertible it suffices to show that \( \xi^j - \xi^k \) is invertible for \( j \neq k \). If this element is not invertible, \( \xi^j - \xi^k \in 2\mathcal{R} \). Recall that the reduction modulo 2 homomorphism \( \overline{\pi} : \mathcal{R} \to \mathbb{F}_{2^r} = \mathcal{R}/2\mathcal{R} \), discussed before Exercise 749, maps the primitive element \( \xi \) of \( \mathcal{R} \) to the primitive element \( \theta \) of \( \mathbb{F}_{2^r} \). Thus \( \overline{\pi}(\xi^j) + \overline{\pi}(\xi^k) = 0 \), implying that \( \theta^j = \theta^k \). But \( \theta^j \neq \theta^k \) for \( j \neq k \) with \( j \) and \( k \) between 0 and \( n-1 \). Thus the elements of \( \mathcal{S}_1 \) are invertible. We now show that the elements of \( \mathcal{S}_1 \) are distinct. Suppose that \( \xi^j - \xi^k = \xi^\ell - \xi^m \) with \( j \neq k \) and \( \ell \neq m \); then

```
1 + \xi^a = \xi^b + \xi^c, \tag{12.24}
```

where \( m - j \equiv a \pmod n \), \( \ell - j \equiv b \pmod n \), and \( k - j \equiv c \pmod n \). So \( (1 + \xi^a)^2 = v_2(1 + \xi^a) = (\xi^b + \xi^c)^2 = v_2(\xi^b + \xi^c) \), implying that \( 1 + \xi^{2a} + 2\xi^a - v_2(1) - v_2(\xi^a) = \xi^{2b} + \xi^{2c} + 2\xi^{b+c} - v_2(\xi^b) - v_2(\xi^c) \), where \( v_2 \) is the Frobenius automorphism. Thus \( 2\xi^a = 2\xi^{b+c} \), and hence \( a = b + c \pmod n \). Therefore if \( x = 0^a \), \( y = 0^b \), and \( z = 0^c \), then \( x = yz \). Applying \( \overline{\pi} \) to (12.24), we also have \( 1 + x = y + z \). Hence \( 0 = 1 + yz + y + z = (1 + y)(1 + z) \) holds in \( \mathbb{F}_{2^r} \), implying \( y = 1 \) or \( z = 1 \). So \( b \equiv 0 \pmod n \) or \( c \equiv 0 \pmod n \). Hence \( \ell = j \) or \( k = j \); as the latter is impossible, we have \( \ell = j \), which yields \( k = m \) as well. So the elements of \( \mathcal{S}_1 \) are distinct.

Finally, we show that the elements of \( \mathcal{S}_1 \cup \mathcal{S}_2 \) are distinct. Assume \( \xi^j - \xi^k = \pm \xi^m \). By rearranging and factoring out a power of \( \xi \), \( 1 + \xi^a = \xi^b \). So \( (1 + \xi^a)^2 = v_2(1 + \xi^a) = \xi^{2b} - v_2(\xi^b) \), giving \( 1 + 2\xi^a + \xi^{2a} - (1 + \xi^{2a}) = \xi^{2b} - \xi^{2b} \). Therefore \( 2\xi^a = 0 \), which is a contradiction.

We now have the tools to find the Lee weight distribution of \( \widehat{\mathcal{K}}(r+1) \), which is also the Hamming weight distribution of the binary Kerdock code \( \mathcal{K}(r+1) = \Phi(\widehat{\mathcal{K}}(r+1)) \) by Theorem 12.2.2.