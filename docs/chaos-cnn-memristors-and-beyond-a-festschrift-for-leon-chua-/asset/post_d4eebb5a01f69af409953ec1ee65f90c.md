
RESULTS FOR THE UNIFORMITY OF P-VALUES AND THE PROPORTION OF PASSING SEQUENCES

generator is `<data/1oz1_4_b1n32_alternes_cirandom_y_x4_31250.txt>`

| C1 | C2 | C3 | C4 | C5 | C6 | C7 | C8 | C9 | C10 | P-VALUE | PROPORTION | STATISTICAL TEST |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 10 | 9 | 10 | 11 | 16 | 8 | 8 | 11 | 4 | 13 | 0.419021 | 100/100 | Frequency |
| 17 | 6 | 13 | 8 | 12 | 7 | 13 | 10 | 8 | 6 | 0.213309 | 100/100 | BlockFrequency |
| 8 | 9 | 13 | 8 | 9 | 11 | 11 | 9 | 12 | 10 | 0.978072 | 99/100 | CumulativeSums |
| 8 | 8 | 12 | 10 | 11 | 10 | 12 | 10 | 7 | 12 | 0.964295 | 99/100 | CumulativeSums |
| 6 | 11 | 15 | 12 | 7 | 12 | 8 | 10 | 12 | 5 | 0.477986 | 99/100 | Runs |
| 11 | 9 | 12 | 7 | 12 | 6 | 9 | 10 | 13 | 11 | 0.867692 | 99/100 | LongestRun |
| 7 | 10 | 16 | 12 | 9 | 8 | 11 | 10 | 12 | 5 | 0.494392 | 99/100 | Rank |
| 8 | 17 | 10 | 6 | 12 | 7 | 13 | 11 | 9 | 7 | 0.334538 | 99/100 | FFT |
| 12 | 7 | 8 | 8 | 6 | 9 | 9 | 9 | 18 | 14 | 0.213309 | 99/100 | NonoverlappingTemplate |
| 12 | 11 | 11 | 9 | 16 | 6 | 10 | 7 | 8 | 10 | 0.616305 | 99/100 | OverlappingTemplate |
| 11 | 9 | 8 | 6 | 10 | 14 | 9 | 13 | 8 | 12 | 0.779188 | 100/100 | Universal |
| 12 | 9 | 8 | 10 | 10 | 16 | 8 | 10 | 12 | 5 | 0.477986 | 99/100 | ApproximateEntropy |
| 5 | 7 | 9 | 5 | 8 | 4 | 5 | 10 | 12 | 4 | 0.452799 | 68/69 | RandomExcursions |
| 4 | 9 | 8 | 9 | 6 | 7 | 6 | 8 | 9 | 11 | 0.063482 | 69/69 | RandomExcursionsVariant |
| 15 | 6 | 12 | 11 | 12 | 8 | 13 | 5 | 9 | 9 | 0.437274 | 98/100 | Serial |
| 9 | 5 | 11 | 11 | 9 | 13 | 9 | 8 | 14 | 11 | 0.739918 | 99/100 | LinearComplexity |

Fig. 15. Successful result of the NIST tests.

![](img/039e7d3c23390584a66737067db8b75b_331_0.png)

![](img/039e7d3c23390584a66737067db8b75b_331_1.png)

(a)

(b)

Fig. 16. (a) Cascader symbol. (b) Two cascading receivers combined.

The last symbol we design in order to schematise mathematically the cascading method is the cascader displayed on Fig. 16(a).

## 4. Mathematical Circuit Engineering

### 4.1. Signal masking

In the limited extent of this chapter, we give only two examples of the engineering of mathematical circuits we have introduced in the previous section. The first one is an improvement of the cascading of two identical receivers of Chua's circuit. Albeit this improvement is rather from a numerical point of view than a practical one, it is given in order to illustrate more in depth the combination of circuit elements. It is possible to combine two cascading receivers as in Fig. 16(b).

The equations of this circuit are

```
{ ẏ5 = x4(t) − y5 + z5
  ż5 = −β y5 }  (34)
ẋ6 = α( y5(t) − x6 − f(x6) )  (35)
{ ẏ7 = x6(t) − y7 + z7
  ż7 = −β y7 }  (36)
ẋ8 = α( y7(t) − x8 − f(x8) )  (37)
```

Then s(t) is recovered as

```
s8(t) = r(t) − x8(t) ≈ s(t)  (38)
```

Numerical experiments show an improvement of the results [1], [19].

### 4.2. Noise-resisting cryptography

The second example which highlights the complex combination of circuit elements belongs to the new flourishing field of chaotic-based cryptography. We proposed last year [2] a novel noise-resisting ciphering method resorting to a chaotic multistream pseudorandom number generator (denoted Cms-PRNG) described below. This Cms-PRNG co-generates an arbitrarily large number of uncorrelated chaotic sequences. These cogenerated sequences are actually used in several steps of the ciphering process. Noisy transmission conditions are considered, with realistic assumptions. The efficiency of the proposed method for ciphering and deciphering is illustrated through numerical simulations based on a Cms-PRNG involving ten coupled chaotic sequences.

![](img/039e7d3c23390584a66737067db8b75b_332_0.png)

Fig. 17. Chaotic multistream PRNG (Cms-PRNG).

The CPRNG described in Fig. 14 can be improved in order to generate uncorrelated sequences of pseudo-random numbers, possessing a large number of keys. This is simply obtained by adding a coupler as a keyer as in the circuit of Fig. 17 corresponding to Eq. (39) for 4-streams, or Eq. (40) for p–streams.

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

The ring coupling, which is expressed as a diagonal matrix in Eq. (31), is completed with numerous other non-vanishing coefficients of the matrix used as secret keys in Eq. (40). Then the originality of the noise-resisting ciphering method introduced, which uses this Cms-PRNG, is twofold. First, a novel ciphering method is proposed aimed at resisting to a noisy transmission channel. The main idea is to establish, between the transmitter and the receiver, a correspondence between the alphabet constituting the plain text and some intervals defining a partition of [−1, 1]. Some realistic assumption about the noise boundedness allows to restrict the bounds of the aforementioned intervals in order to precisely resist to the effects of the noise. An extra scrambling resorting to a co-generated chaotic sequence enhances the ciphering process. Then a new chaotic substitution method is developed: considering a chaotic carrier, belonging to the set of cogenerated and coupled pseudo-random chaotic sequences, the idea is to randomly/chaotically (in fact, this is determined by a second pseudo-random chaotic sequence) replace some elements of the carrier by a ciphered element (a letter here) of the message. At the receiver end, a copy of the Cms-PRNG, with the same parameters (hence we deal with a symmetrical ciphering method) allows to generate the necessary chaotic sequences and therefore to retrieve the initial message.

This process can be summarized in both circuits of Figs. 18, 19. Due again to the limited extent of this chapter, we cannot expand these figures in order to show the constituting symbols in each oval-shaped region of the circuit. The originality of the method lies in the use of a chaotic pseudo-random number generator: several co-generated sequences can be used at different steps of the ciphering process, since they present the strong property of being uncorrelated. Each letter of the initial alphabet of the plain text is encoded as a subinterval of [−1, 1]. The bounds of each interval are defined in function of the known bound of the additive noise.

![](img/039e7d3c23390584a66737067db8b75b_333_0.png)

![](img/039e7d3c23390584a66737067db8b75b_333_1.png)

A pseudo-random sequence is used to enhance the complexity of the ciphering. The transmission consists of a substitution technique inside a chaotic carrier, depending on another cogenerated sequence. The efficiency of the proposed scheme is illustrated on some numerical simulations [2]. As further work, some studies should be performed on several sets of unknown parameters, since with the considered Cms-PRNG with 10 states, the number of possible parameters amounts to 90 (the εᵢ,ⱼ and the kᵢ).

## 5. Conclusion

Following the worldwide tradition of use of Chua’s circuits for various purposes, we have introduced the paradigm of chaotic mathematical circuitry which shows some similarity to the paradigm of electronic circuitry—the design of electronic circuits. This new paradigm allows, as an example, the building of new chaotic and random number generators. In this beginning of the third Millennium, the old tradition of design of electronic circuits is drastically revolutionized by the introduction by L. O. Chua of new components with memory, namely memristor, memcapacitor and meminductor. These devices are common at the nanoscale and their combination in circuits open up new functionalities in electronics. Apart from the obvious use of these elements in nonvolatile memories, several applications can be already envisioned, especially in neuromorphic devices to stimulate learning, adaptative and spontaneous behavior [7].

Alongside this electronic circuits revolution, the new theory of mathematical circuits allows many new applications in chaotic cryptography, genetic algorithms in optimization and in control, … Due to the versatility of the new
