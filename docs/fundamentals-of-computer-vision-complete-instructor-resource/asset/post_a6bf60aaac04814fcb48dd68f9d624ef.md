
### 3.3.3 Simulated Annealing

We will base much of the following discussion of minimization techniques on an algorithm known as “simulated annealing” (SA), which proceeds below as Algorithm 3.1. (See the book by Aarts and van Laarhoven for more detail [3.4].)

```
Algorithm 3.1: Simulated annealing.
Data: Choose (at random) an initial value of x, and an initial value of T > 0.
Result: x̂ that minimizes H.
1 while T > Tmin do
2     Generate a point y which is a “neighbor” of x. (The exact definition of “neighbor” will be discussed soon.);
3     if H(y) < H(x) then
4         Replace x with y;
5         also denoted as “accepting y”
6     end
7     else
8         Compute Py = exp(−(H(y)−H(x))/T);
9         if Py ≥ R then
10            Replace x with y, where R is a random number uniformly distributed between 0 and 1;
11        end
12    end
13    Decrease T slightly;
end
```

Simulated annealing is most easily understood in the context of combinatorial optimization. In this case, one definition of a “neighbor” of a vector x is another vector y, such that only one of the elements of x is changed (discretely) to create y.12 Thus, if x is binary and of dimension d, one may choose a neighbor y = x ⊕ z, where z is a binary vector in which exactly one element is non-zero, and that element is chosen at random, and ⊕ represents exclusive OR.

In lines 3 through 5 of the algorithm, we perform a descent. Thus we “always fall down hill.”

In lines 7 through 10, we provide a mechanism for sometimes making uphill moves. Initially, we ignore the parameter T and note that if y represents an uphill move, the probability of accepting y is proportional to exp(−(H(y) − H(x))). Thus, uphill moves can occur, but are exponentially less likely to occur as the size of the uphill move becomes larger. The likelihood of an uphill move is, however, strongly influenced by T. Consider the case that T is very large. Then (H(y)−H(x))/T ≤ 1 and Py ≈ 1. Thus, all moves will be accepted. As T is gradually reduced, uphill moves become gradually less likely until for low values of T (T << (H(y) − H(x)), such moves are essentially impossible.

| sum | | number of ways |
|---|---|---|
| 0 | | 0 |
| 1 | | 1 |
| 2 | 1-1 | 1 |
| 3 | 2-1,1-2 | 2 |
| 4 | 1-3,3-1,2-2 | 3 |
| 5 | 2-3,3-2,4-1,1-4 | 4 |
| 6 | 1-5,5-1,2-4,4-2,3-3 | 5 |
| 7 | 3-4,4-3,2-5,5-2,6-1,1-6 | 6 |
| 8 | 2-6,6-2,3-5,5-3,4-4 | 5 |
| 9 | 3-6,6-3,4-5,5-4 | 4 |
| 10 | 4-6,6-4,5-5 | 3 |
| 11 | 5-6,6-5 | 2 |
| 12 | 6-6 | 1 |

Figure 3.4 The possible ways to roll two dice.

One may consider an analogy to physical processes in which the state of each variable (one or zero) is analogous to the spin of a particle (up or down). At high temperatures, particles randomly change state, and if temperature is gradually reduced, minimum energy states are achieved. The parameter _T_ in Algorithm 3.1 is thus analogous to (and often referred to as) temperature, and this minimization technique is therefore called “simulated annealing.”

## 3.4 A Brief Review of Probability

Let us imagine a statistical experiment: rolling two dice. It is possible to roll any number between two and twelve (inclusive), but as we know, some numbers are more likely than others. To see this, consider the possible ways to roll a five.

We see from Figure 3.4 that there are four possible ways to roll a five with two dice. Each event is independent. That is, the chance of rolling a two with the second die does not depend at all on what is rolled with die number 1.

Independence of events is an important implication. It means that the joint probability of the two events is equal to the product of their individual probabilities, and the conditional probabilities:

```
Pr(a, b) = Pr(a|b)Pr(b) = Pr(a)Pr(b) = Pr(b|a)Pr(a). (3.56)
```

In Eq. 3.56, the symbols _a_ and _b_ represent events, e.g., the rolling of a six. Pr(_b_) is the probability of such an event occurring, and Pr(_a_|_b_) is the conditional probability of event _a_ occurring, given that event _b_ has occurred.

In Figure 3.4, we tabulate all the possible ways of rolling two dice, and show the resulting number of different ways that the numbers from 2 to 12 can occur. We note that 6 different events can lead to a 7 being rolled. Since each of these events is equally probable (1 in 36),

![](img/5f95dd954ac63cc68119f6f48ca99e18_50_0.png)

Figure 3.5 The information of Figure 3.4 in graphical form.

then a 7 is the most likely roll of two dice. In Figure 3.5 the information from Figure 3.4 is presented in graphical form.

In Computer Vision, we are most often interested in the probability of a particular measurement occurring. We have a problem, however, when we try to plot a graph such as Figure 3.5 for a continuously valued function. For example, how do we ask the question: “What is the probability that a man is six feet tall?” Clearly, the answer is zero, for an infinite number of possibilities could occur arbitrarily close to 6.0 feet (we might equally well ask, “What is the probability that a man is (exactly) 6.31459267 feet tall?”). Still, we know intuitively that the likelihood of a man being six feet tall is higher than the likelihood of his being ten feet tall. We need some way of quantifying this intuitive notion of likelihood.

One question that does make sense is, “What is the probability that a man is **less than** six feet tall?” Such a function is referred to as a **probability distribution function**

```
P(x) = Pr(h < x) (3.57)
```

for some measurement, h. Figure 3.6 illustrates the probability distribution function for the result of rolling two dice.

![](img/5f95dd954ac63cc68119f6f48ca99e18_51_0.png)

Figure 3.6 The probability distribution of Figure 3.5, showing the probability of rolling two dice to get a number LESS than x. Note that the curve is steeper at the more likely numbers.

Another well-formed question would be, “What is the probability that a man’s height is between x and x + Δx?” Such a question is easily answered in terms of the density function:

```
Pr(x ≤ h < x + Δx) = Pr(h < x + Δx) - Pr(h < x) = P(x + Δx) - P(x)
```

Dividing by Δx and taking the limit as Δx → 0, we see that we may define the *probability density function* as the derivative of the distribution function:

```
p(x) = \frac{d}{dx}P(x) (3.58)
```

where p(x) has all the properties that we desire. It is well defined for continuously valued measurements and it has a maximum value for those values of the measurement that are intuitively most likely. Furthermore,

```
\int_{-\infty}^{\infty} p(x)dx = 1 (3.59)
```

which we must require, since **some** value will certainly occur.

## 3.5 Assignments

Assignment 3.1: Determine whether the functions sin x and sin 2x might be orthonormal or orthogonal functions.

Assignment 3.2: Find the OT corresponding to a counterclockwise rotation of 30° about the z axis. Prove the columns of the resulting matrix are a basis for R³.

Assignment 3.3: Prove Eq. 3.17. Hint: Use Eq. 3.13. Eq. 3.15 might be useful as well.

Assignment 3.4: A positive definite matrix has positive eigenvalues. Prove this. (For that matter, is it even true?)

Assignment 3.5: In section 3.2.2, we defined a peculiar set of scalars, called S, and coupled it with two strange operations called * and +, and speculated that might be a vector space. One example was given, which showed that it might possibly be. What do you think? Can you find a counterexample?

Assignment 3.6: In section 3.2.2, we defined a peculiar set of scalars, called S, and coupled it with two strange operations called * and +, and speculated that might be a vector space. How would you define orthogonality in this space? Would you have to find something that acts like zero? How would you define an inner product? Discuss.

Assignment 3.7: Does the function y = xe⁻ˣ have a unique value x that minimizes y? If so, can you find it by taking a derivative and setting it equal to zero? Suppose this problem requires gradient descent to solve. Write the algorithm you would use to find the x that minimizes y.

Assignment 3.8: We need to solve a minimization problem using gradient descent. The function we are minimizing is sin x + ln y. Which of the following is the expression for the gradient that you need in order to do gradient descent?
(a) cos x + 1/y   (b) y = -cos x / -1/x   (c) -∞
(d) [cos x; 1/y]   (e) ∂/∂x sin x + ∂/∂y ln y

Assignment 3.9: (a) Write the algorithm that uses gradient descent to find the vector [x, y]ᵀ that minimizes the function z = x exp(-(x² + y²)). (b) Write a computer program that finds the minimizing x, y pair.

Assignment 3.10: Find the minimum of y = 50 sin(x) + x² over -10 ≤ x ≤ 10. Use both gradient descent (GD) and simulated annealing (SA) to locate the minimum. This assignment intends to give students hands-on experience on how GD and SA work and how GD can get trapped at the local minimum but SA is capable of arriving at the global minimum regardless of the initial starting point.

- 1. Use MATLAB to plot this function. Visually observe the multiple local minima and the global minimum within the given interval of x.

- 2. Implement GD and test the code under the following parameter setups.

- (a) Pick a starting point at x = 7. What is the minimum?
