# Algorithm 8.1 Single-layer perceptron learning

Input: Training data X = {x1,⋯,xN} and associated labels {t1,⋯,tN}; {xn ∈ ℝD, tn ∈ {0,1}}; learning rate η > 0.

Output: A trained single-layer perceptron with optimal set of weights w.

```
1: Randomly initialize the set of weight w = (w1,⋯,wd) to zero.
2: repeat
3:   for n in {1,...,N} do
4:     Compute the neuron output on = sign(wᵗ xn)
5:     if on ≠ tn then
6:       w ← w + η xn      # misclassified data
7:     end if
8:   end for
9: until All training data are correctly satisfied or a specified minimum number of iterations are executed
```

perceptron criterion is equivalent to solving the linear inequality tn wᵗ xn > 0 for all xn, which can be done either incrementally, one sample at a time, or in batch fashion.

The SLP learning is shown in Algorithm 8.1. It is a equivalent to stochastic gradient descent on the perceptron criterion. Some variants of the algorithm use a linearly decreasing learning rate η(n) as function of n. For each misclassified sample xn, the training process adds the data to the weight when data belong to class C2 and subtracts the input data from the weights, when the data belong to C1. The effect of this label-based selective update is to incrementally re-align the separating hyperplane to the direction that optimally separates the two classes [19,35]. The batch version of the perceptron algorithm performs a similar update on the accumulated sum of misclassified samples:

```
w ← w + η(t) Σ_{n, o_n ≠ t_n} x_n t_n    (8.21)
```

for a linearly decreasing learning η(t) as a function of training time t. The update is done up to a specified number of epochs or when all data have been correctly classified. It is a direct application of the delta rule since weights are updated according to their contribution to the error.

The perceptron convergence theorem guarantees the optimality of the process: The learning algorithm, as illustrated in Algorithm 8.1, will find the optimal set of weights within a finite number of iterations, provided that the classes are linearly separable [35,52,114].

For non-linear problems, there is no guarantee of success. In that scenario, learning is aimed at achieving classification performance within a tolerable margin of error γ, such that

```
t_n wᵗ x_n > γ    (8.22)
```

for all n. The perceptron learning then minimizes misclassification error relative to that margin, which gives

```
w ← w + η x_n    if − t_n wᵗ x_n > γ.    (8.23)
```

For a γ > 0 satisfying the condition in Equation 8.22, the perceptron margin theorem provides a bound on the number of achievable errors. Suppose there exists a normalized set of weights w such that || w || = 1 and that the entire training set is contained in a ball of diameter D (|| x_n || < D for all n), then the number of mistakes M on the training set X made by the perceptron learning algorithm is at most D²/γ². However, a priori knowledge of the optimal γ is hardly available. In practice, γ can be set to

```
γ = min_n t_n wᵗ x_n    (8.24)
```