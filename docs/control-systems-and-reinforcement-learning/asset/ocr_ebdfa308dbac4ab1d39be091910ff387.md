# 4.10 Exercises

Review Exercise 4.8 before proceeding: Success will require some mechanism to ensure boundedness of your estimates (neither $\Gamma$ nor its derivative is Lipschitz continuous).

+   (a) Experiment with each of the three qSGSD algorithms, provide plots of the estimates as a function of time, and comment on your initial findings. Decide on your favorite algorithm for the remainder of the exercise.

+   (b) Comment on how the rate of convergence is impacted by $\epsilon$ for $\Theta_0 > 2$, and the likelihood of becoming trapped with $\Theta_0 < -10$ (here $\epsilon > 0$ scales the probing signal in each of the qSGSD algorithms).

+   Obtain a plot of your estimate $	heta_t^*$ as a function of $\epsilon$ for $\Theta_0 > 2$, and comment on observed bias.

+   (c) See if you can design a time-varying sequence $\{\epsilon_t\}$ that results in a reliable algorithm that is convergent for any initial condition $\Theta_0$.

+   Test your design with the modified $\Gamma_m(x) = x^2(1+(x+m)^2)$ for a range of values of $m$ (say, $m \in \{-4, 4, 8\}$).

4.14 Consider the MagBall example introduced in Section 2.7.3. This is Exercise 2.19. Our goal is to reach the least possible distance $r_0$ from the magnet.

Our approach is to gradient-free optimization: $c(x, u) = \hat{y}^2 + u^2$, where $\hat{y} = x_1-r_0$. Propose a policy of $u = \phi^0(x)$, based on your insight from Exercise 2.19, and minimize $\mathbb{E}[J_p(X)]$ using qSGSD (and surrounding discussion).

4.15 Exercise 3.10, with the introduction of a cost $c(x, u) = \|x\|^2 + u^2$. Based on your insight from Exercise 3.10, propose a policy of $u = \phi^	heta(x), 	heta \in \mathbb{R}^d$ (choose $d \le 4$). Obtain an approximation of the minimum of $\mathbb{E}[J_p(X)]$ using qSGSD.

4.16 Optimization of the Running Game. Rather than LQR, in Exercise 3.9, optimize $(K_p, K_i, K_v)$ using qSGSD. Your results seem similar to what was obtained in Exercise 3.9 when $N$ is large?

4.17 This (as well as Exercise 4.16) clarifies the relevance at the close of Section 4.7.2: When we search for policies that are optimal within a specific class, we are forced to abandon dynamic programming and use optimization techniques as qSGSD.

The state evolves on $X = \mathbb{R}^*$, in continuous time, in which the derivative of each state is directly influenced by the single input and a noise:

```
$\dot{x}_t(i) = x_t(i-1) + u_t(i), \quad 1 \le i \le n,$
```

where not denotes $x_t(0) = 0$. The cost function is quadratic, of the form $c(x, u) = \|x\|^2 + ru^2$ with $r > 0$.

+   (a) The $n 	imes n$ feedback gain $K^*$ for a range of $n_s$, and see if you can discover any structure. What happens for very small or large $r$?

+   (c) We next obtain an optimal gain over a restricted class of policies: $u_t(i) = - 	heta_{xt}(i)$ for each $i$ and $t$. Dev a QSA ODE to find $	heta^*$, and for a range of $r$ compare the performance of your solution to what was obtained in (a). This, you must compute the value function $J$ associated with your policy and compare it to $J^*$.

4.18 Consider the linear QSA ODE with noise (4.8):

```
$\dot{\Theta}_t = a_t f(\Theta_t, \xi_t) = a_t[A_0 + \xi_t A_1]\Theta_t,$
```

$\xi_t = \sin(\omega t + \phi)$.