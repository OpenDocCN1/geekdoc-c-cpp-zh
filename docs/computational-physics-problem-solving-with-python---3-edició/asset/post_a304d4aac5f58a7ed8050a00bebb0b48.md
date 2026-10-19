
### 2.5.2 Implementation and Assessment

where “term” is the last term kept in the series (2.27) and “sum” is the accumulated sum of all the terms. In general, you are free to pick any tolerance level you desire, although if it is too close to, or smaller than, machine precision, your calculation may not be able to attain it. A pseudocode for performing the summation is

```text
term = x, sum = x, eps = 10^(-8)   # Initialize
do
    term = -term*x*x/(2n+1)/(2n)   # New term from old
    sum = sum + term               # Add term
while abs(term/sum) > eps          # Break iteration
end do
```

- **1.** Write a program that implements this pseudocode for the indicated \(x\) values. Present the results as a table with headings \(x\), sum, \(|sum - \sin(x)|/\sin(x)\), where \(\sin(x)\) is the value obtained from the built-in function. The last column here is the relative error in your computation. Modify the code that sums the series in a “good way” (no factorials) to one that calculates the sum in a “bad way” (explicit factorials).
- **2.** Produce a table as above.
- **3.** Start with a tolerance of \(10^{-8}\) as in (2.29).
- **4.** Show that for sufficiently small values of \(x\), your algorithm converges (the changes are smaller than your tolerance level) and that it converges to the correct answer.
- **5.** Compare the number of decimal places of precision obtained with that expected from (2.29).
- **6.** Without using the identity \(\sin(x + 2n\pi) = \sin(x)\), show that there is a range of somewhat large values of \(x\) for which the algorithm converges, but that it converges to the wrong answer.
- **7.** Show that as you keep increasing \(x\), you will reach a regime where the algorithm does not even converge.
- **8.** Now make use of the identity \(\sin(x + 2n\pi) = \sin(x)\) to compute \(\sin x\) for large \(x\) values where the series otherwise would diverge.
- **9.** Repeat the calculation using the “bad” version of the algorithm (the one that calculates factorials) and compare the answers.
- **10.** Set your tolerance level to a number smaller than machine precision and see how this affects your conclusions.

## 3 Errors and Uncertainties in Computations

> *To err is human, to forgive divine.*
>
> — Alexander Pope

Whether you are careful or not, errors and uncertainties are part of computation. Some errors are the ones that humans inevitably make, but some are introduced by the computer. Computer errors arise because of the limited precision with which computers store numbers or because algorithms or models can fail. Although it stifles creativity to keep thinking “error” when approaching a computation, it certainly is a waste of time, and possibly harmful, to work with results that are meaningless “garbage” because of errors. In this chapter, we examine some of the errors and uncertainties that may occur in computations. Although we do not keep repeating a mantra about watching for errors, the lessons of this chapter apply to all other chapters as well.

### 3.1 Types of Errors (Theory)

Let us say that you have a program of high complexity. To gauge why errors should be of concern, imagine that the program has the logical flow

\[
\text{start} \to U_1 \to U_2 \to \cdots \to U_n \to \text{end}, \qquad (3.1)
\]

where each unit \(U\) might be a statement or a step. If each unit has probability \(p\) of being correct, then the joint probability \(P\) of the whole program being correct is \(P = p^n\). Let us say, we have a medium-sized program with \(n = 1000\) steps and that the probability of each step being correct is almost 1, \(p \simeq 0.9993\). This means that you end up with \(P \simeq 1/2\), that is, a final answer that is as likely wrong as right (not a good way to build a bridge). The problem is that, as a scientist, you want a result that is correct – or at least in which the uncertainty is small and of known size, even if the code executes millions of steps.

Four general types of errors exist to plague your computations:

- **1. *Blunders or bad theory*:** Typographical errors entered with your program or data, running the wrong program or having a fault in your reasoning (theory), using the wrong data file, and so on. (If your blunder count starts increasing, it may be time to go home or take a break.)
- **2. *Random errors*:** Imprecision caused by events such as fluctuations in electronics, cosmic rays, or someone pulling a plug. These may be rare, but you have no control over them and their likelihood increases with running time; while you may have confidence in a 20 s calculation, a week-long calculation may have to be run multiple times to check reproducibility.
- **3. *Approximation errors*:** Imprecision arising from simplifying the mathematics so that a problem can be solved on the computer. They include the replacement of infinite series by finite sums, infinitesimal intervals by finite ones, and variable functions by constants. For example,

\[
\sin(x) = \sum_{n=1}^{\infty} \frac{(-1)^{n-1} x^{2n-1}}{(2n-1)!} \qquad \text{(exact)}
\]
\[
\simeq \sum_{n=1}^{N} \frac{(-1)^{n-1} x^{2n-1}}{(2n-1)!} + \mathcal{E}(x,N) \qquad \text{(algorithm)}, \tag{3.2}
\]

where \(\mathcal{E}(x,N)\) is the approximation error and is the series from \(N+1\) to \(\infty\). Because the approximation error arises from the algorithm we use to approximate the mathematics, it is also called the *algorithmic error*. For every reasonable approximation, the approximation error should decrease as \(N\) increases and should vanish in the limit \(N \to \infty\). Specifically for (3.2), because the scale for \(N\) is set by the value of \(x\), a small approximation error requires \(N \gg x\). So if \(x\) and \(N\) are close in value, the approximation error will be large.

- **4. *Round-off errors*:** Imprecision arising from the finite number of digits used to store floating-point numbers. These “errors” are analogous to the uncertainty in the measurement of a physical quantity encountered in an elementary physics laboratory. The overall round-off error accumulates as the computer handles more numbers, that is, as the number of steps in a computation increases. This may cause some algorithms to become *unstable* with a rapid increase in error. In some cases, round-off error may become the major component in your answer, leading to what computer experts call *garbage*.

  For example, if your computer kept four decimal places, then it will store 1/3 as 0.3333 and 2/3 as 0.6667, where the computer has “rounded off” the last digit in 2/3. Accordingly, if we ask the computer to do as simple a calculation as \(2(1/3) - 2/3\), it produces

  \[
  2\left(\frac{1}{3}\right) - \frac{2}{3} = 0.6666 - 0.6667 = -0.0001 \neq 0. \tag{3.3}
  \]

  So although the result is small, it is not 0, and if we repeat this type of calculation millions of times, the final answer might not even be small (small garbage begets large garbage).

When considering the precision of calculations, it is good to recall our discussion in Chapter 2 of significant figures and scientific notation given in your early physics or engineering classes. For computational purposes, let us consider how the computer may store the floating-point number

\[
a = 11\,223\,344\,556\,677\,889\,900 = 1.122\,334\,455\,667\,788\,99 \times 10^{19}. \tag{3.4}
\]

Because the exponent is stored separately and is a small number, we may assume that it will be stored in full precision. In contrast, some of the digits of the mantissa may be truncated. In double precision, the mantissa of \(a\) will be stored in two words, the most significant part representing the decimal 1.12233, and the least significant part 44 556 677. The digits beyond 7 are lost. As we shall see soon, when we perform calculations with words of fixed length, it is inevitable that errors will be introduced (at least) into the least significant parts of the words.

#### 3.1.1 Model for Disaster: Subtractive Cancellation

Calculations employing numbers that are stored only approximately on the computer can only be expected to yield approximate answers. To demonstrate the effect of this type of uncertainty, we model the computer representation \(x_c\) of the exact number \(x\) as

\[
x_c \approx x(1 + \varepsilon_x). \tag{3.5}
\]

Here \(\varepsilon_x\) is the relative error in \(x_c\), which we expect to be of a similar magnitude to the machine precision \(\varepsilon_m\). If we apply this notation to the simple subtraction \(a = b - c\), we obtain

\[
a = b - c \Rightarrow a_c \approx b_c - c_c \approx b(1 + \varepsilon_b) - c(1 + \varepsilon_c)
\]
\[
\Rightarrow \frac{a_c}{a} \approx 1 + \varepsilon_b \frac{b}{a} - \frac{c}{a} \varepsilon_c. \tag{3.6}
\]

We see from (3.6) that the resulting error in \(a\) is essentially a weighted average of the errors in \(b\) and \(c\), with no assurance that the last two terms will cancel. Of special importance here is the observation that the error in the answer \(a_c\) increases when we subtract two nearly equal numbers (\(b \approx c\)) because then we are subtracting off the most significant parts of both numbers and leaving the error-prone least-significant parts:

\[
\frac{a_c}{a} \triangleq 1 + \varepsilon_a \approx 1 + \frac{b}{a}(\varepsilon_b - \varepsilon_c) \approx 1 + \frac{b}{a} \max(|\varepsilon_b|, |\varepsilon_c|). \tag{3.7}
\]

This shows that even if the relative errors in \(b\) and \(c\) cancel somewhat, they are multiplied by the large number \(b/a\), which can significantly magnify the error. Because we cannot assume any sign for the errors, we must assume the worst (the “max” in (3.7)).
