# 6.2 A Class of Without-Memory Methods

In 2015 Guo and Qian followed the two-point methods without memory (GQM) [11]:

\begin{cases} w_k = x_k + f(x_k), y_k = x_k - \dfrac{f(x_k)}{f[x_k, w_k]}, \quad k = 0,1,2,\dots, \\ x_{k+1} = y_k - \dfrac{(x_k - y_k)(x_k - w_k)(y_k - w_k)f(y_k)}{(y_k - w_k)^2 f(x_k) + (x_k - w_k)(x_k - 2y_k + w_k)f(y_k) - (x_k - y_k)^2 f(w_k)}. \end{cases} (6.1)

The next theorem states the error equations in the methods in Equation (6.1).

# Theorem 6.1 Let I ⊆ ℝ be an open interval, f : I → ℝ be a scalar function which has a simple root α in the open interval I, and also the initail approximation x₀ is sufficiently close the simple zero, then the iteration method defined by (1) is of fourth-order convergence and it satisfies the error equation below:

e_{k+1} = (1 + f'(α))^2 c_2 (c_2^2 - c_3) e_k^4 + O(e_k^5). (6.2)

# Proof 6.1 The proof is given in Guo and Qian [11].

By imposing two parameters in the method described in Equation (6.1), the family of two-parameters without-memory method of the following fourth-order result (TKM4):

\begin{cases} w_k = x_k + γ f(x_k), y_k = x_k - \dfrac{f(x_k)}{f[x_k, w_k] + λ f(w_k)}, \quad k = 0,1,2,\dots, \\ x_{k+1} = y_k - \dfrac{(x_k - y_k)(x_k - w_k)(y_k - w_k)f(y_k)}{(y_k - w_k)^2 f(x_k) + (x_k - w_k)(x_k - 2y_k + w_k)f(y_k) - (x_k - y_k)^2 f(w_k)}. \end{cases} (6.3)

Where γ ∈ ℝ. The next theorem states the error equations in the methods of Equation (6.3).

# Theorem 6.2 Let I ⊆ ℝ be an open interval, f : I → ℝ be a scalar function which has a simple root α in the open interval I, and also the initail approximation x₀ is sufficiently close the simple zero, then, the iteration method (3) has fourth-order convergence and satisfies the following error equation:

e_{k+1} = (1 + f'(α)γ)^2 (λ + c_2)(c_2(λ + c_2) - c_3) e_k^4 + O(e_k^5). (6.4)

whererin c_k = f^k(α)/k!, ∀k ∈ {2,3,4,⋯}, e_k = x_k - α and λ, γ are two real valued free parameters.

# Proof 6.2 Using Taylor's series and symbolic computation; we can determine the asymptotic error constant of the two-step without memory family of methods (3). Now we expand f(x_k) about the simple zero α. Hence, we have

f(x_k) = f'(α)[e_k + c_2 e_k^2 + c_3 e_k^3 + c_4 e_k^4 + O(e_k^5)], (6.5)