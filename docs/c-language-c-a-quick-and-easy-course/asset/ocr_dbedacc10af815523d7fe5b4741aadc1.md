prime numbers in the divisions, those that have had remainder zero, it will be the LCM.

12) When developing your program to calculate the numbers of Bernoulli, the first program in history, Ada Byron realized that, from the series shown first in the formulas with the sum below, she could isolate the values Bₙ, as shown in the second formula, II, which are the Bernoulli numbers. The challenge here is to build a program that calculates and prints the result of these numbers up to a given value, for example n = 10, i. e., the numbers B₀, B₁, B₂, B₃, … B₁₀, starting from B₀ = 1. The reader should not be surprised that the even index numbers, after B₂, are all null, because that is the nature of the sequence. The results should be in fraction form, as the default for this sequence, and the Ada formula, by the way, already has a denominator n+1. We should recall that the

number of combinations of m elements taken k at a time is given by C(m k) = m! / (k!(m-k)!) and, thus, C(n+1 k) = (n+1)! / (k!(n+1-k)!). You can make use of the factorial function, of the example-program #13A, but may find it more appropriate to use something simpler, given that combination of m elements taken k at a time is the product operator of m-i, i from zero to k-1, divided by the product operator of k-i, i from zero to k-1. Ada says that, by limitation of the machine, she omitted the negative sign before the Bₙ formula. With the current machines we can work with sign, changing the value 1 of the numerator by -1. You will need to build also a small routine to add and, with the HCF (example-program #9B), to simplify the fractions that appear as a result.

(I) x/(e^x - 1) = Σ_{n≥0} Bₙ / n! xⁿ
(II) Bₙ = 1/(n+1) Σ_{k=0}^{n} (-1)^k C(n+1 k) B_k

# APPENDIX A

# Examples with reserved words

This section presents mini-programs for 32 reserved words in ANSI C. They all need to be started with the #include <stdio.h>, at least.

```
auto
void Algar() {auto int i; for(i=0;i<10;i++) printf("%d",i);}
main() {Algar();}
```

```
break
main() {char c;int i; for(i=1;i<=1000;i++){c=getchar();
if(c=='\n') break; else printf("\a");}}
```