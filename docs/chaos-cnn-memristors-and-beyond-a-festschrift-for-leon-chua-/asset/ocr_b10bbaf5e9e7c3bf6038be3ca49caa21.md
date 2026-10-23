![](bbox=[0.24, 0.08, 0.76, 0.22])

Fig. 17. Chaotic multistream PRNG (Cms-PNRG).

flourishing field of chaotic based cryptography. We proposed last year [2] a novel noise-resisting ciphering method resorting to a chaotic multistream pseudorandom number generator (denoted Cms-PRNG) described below. This Cms-PRNG co-generates an arbitrarily large number of uncorrelated chaotic sequences. These cogenerated sequences are actually used in several steps of the ciphering process. Noisy transmission conditions are considered, with realistic assumptions. The

efficiency of the proposed method for ciphering and deciphering is illustrated through numerical simulations based on a Cms-PRNG involving ten coupled chaotic sequences.

The CPRNG decribed in Fig. 14, can be improved in order to generate uncorrelated sequences of pseudo-random numbers, possessing a large number of keys. This is simply obtained by adding a coupler as a keyer as in the circuit of Fig. 17 corresponding to Eq. (39) for 4-streams, or Eq. (40) for p–streams.

```
⎧ x_{n+1}^1 = 1 − 2|x_n^1| + k_1(1 − ε_{1,3} − ε_{1,4})x_n^2 + ε_{1,3}x_n^3 + ε_{1,4}x_n^4
x_{n+1}^2 = 1 − 2|x_n^2| + k_2(1 − ε_{2,4} − ε_{2,1})x_n^3 + ε_{2,4}x_n^4 + ε_{2,1}x_n^1
x_{n+1}^3 = 1 − 2|x_n^3| + k_3(1 − ε_{3,1} − ε_{3,2})x_n^4 + ε_{3,1}x_n^1 + ε_{3,2}x_n^2
x_{n+1}^4 = 1 − 2|x_n^4| + k_4(1 − ε_{4,2} − ε_{4,3})x_n^1 + ε_{4,2}x_n^2 + ε_{4,3}x_n^3
(39)
```

```
⎧ x_{n+1}^1 = 1 − 2|x_n^1| + k_1( (1 − Σ_{j=3}^p ε_{1,j}) x_n^2 + Σ_{j=3}^p ε_{1,j}x_n^j )
⋮
x_{n+1}^m = 1 − 2|x_n^m| + k_m( (1 − Σ_{j=1,j≠m,m+1}^p ε_{m,j}) x_n^{m+1} + Σ_{j=1,j≠m,m+1}^p ε_{m,j}x_n^j )
⋮
x_{n+1}^{p−1} = 1 − 2|x_n^{p−1}| + k_{p−1}( (1 − Σ_{j=1}^{p−2} ε_{p−1,j}) x_n^p + Σ_{j=1}^{p−2} ε_{p−1,j}x_n^j )
x_{n+1}^p = 1 − 2|x_n^p| + k_p( (1 − Σ_{j=1}^{p−2} ε_{p,j}) x_n^1 + Σ_{j=1}^{p−2} ε_{p,j}x_n^j )
(40)
```

The ring coupling which is expressed as a diagonal matrix in Eq. (31) is completed with numerous other non vanishing coefficients of the matrix used as secret keys in Eq. (40). Then the originality of the noise-resisting ciphering method

introduced which uses this Cms-PRNG is twofold. First a novel ciphering method is proposed aimed at resisting to a noisy transmission channel. The main idea is to establish, between the transmitter and