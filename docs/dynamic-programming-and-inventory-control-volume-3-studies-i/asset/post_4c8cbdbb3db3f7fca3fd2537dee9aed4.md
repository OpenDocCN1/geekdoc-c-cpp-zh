
Since all the functions are positive, the limit is well defined, but may take the value \( +\infty \). Recalling Lemma 4.2, we can assert that the function \( w_0(x) \) is also l.s.c. We will use in the sequel the assumption (4.3.6)

(4.3.6)
\( w_0(x) < \infty, \forall x. \)
\( u_0(x) \text{ is bounded on bounded sets} \)

## 4.3.3. BELLMAN EQUATION.

We consider the functional equation

(4.3.7)
\( u(x) = \inf_{v \in U} [l(x, v) + \alpha \Phi^v u(x)], \forall x. \)

This equation is now considered, without any interpretation as the value function of a control problem. We state the main result

### Theorem 4.3.
Under the assumptions (4.3.1), (4.3.2), (4.3.6) the set of solutions of the functional equation (4.3.7) satisfying

\( 0 \le u(x) \le w_0(x) \forall x, \)

is not empty and has a minimum and a maximum solution, denoted respectively \( \underline{u}(x) \) and \( \overline{u}(x) \). The minimum solution is l.s.c.

**PROOF.** Consider the following iteration

\( u_0(x) = 0, \)
\( u_{n+1}(x) = \inf_{v \in U} [l(x, v) + \alpha \Phi^v u_n(x)]. \)

This sequence is monotone increasing. We have

\( 0 \le u_n(x) \le w_0(x) \forall x, \)

which can be checked recursively. We thus have \( u_n(x) \uparrow u(x) \) hence

\( u_{n+1}(x) \le \inf[(l(x, v) + \alpha \Phi^v u(x)], \forall x, \)

and thus also

\( u(x) \le \inf[(l(x, v) + \alpha \Phi^v u(x)], \forall x. \)

Moreover, thanks to the assumptions (4.3.2) the functions \( u_n(x) \) are l.s.c. so there exists a Borel map \( v_n(x) \) such that

\( u_{n+1}(x) = l(x, v_n(x)) + \alpha \Phi^{v_n(x)} u_n(x). \)

Let \( n \le m \) we can write

\( u_{m+1}(x) = l(x, v_m(x)) + \alpha \Phi^{v_m(x)} u_m(x) \)
\( \ge l(x, v_m(x)) + \alpha \Phi^{v_m(x)} u_n(x), \)

hence also

\( u(x) \ge l(x, v_m(x)) + \alpha \Phi^{v_m(x)} u_n(x). \)

Now for \( x \) fixed, the sequence \( v_m(x) \) remains in a compact set and thus there exists a subsequence such that \( v_{m_k}(x) \to v^*(x) \). Remember that \( n \) is fixed and that \( l(x, v) + \alpha \Phi^v u_n(x) \) is l.s.c.

We thus can state

\( u(x) \ge l(x, v^*(x)) + \alpha \Phi^{v^*} u_n(x). \)

Letting now \( n \) go to \( \infty \) we obtain

\( u(x) \ge l(x, v^*(x)) + \alpha \Phi^{v^*} u(x), \)

hence

\(u(x) \ge \inf_v [l(x, v) + \alpha \Phi^v u(x)]\).

Since the reverse inequality is true, the function \(u\) is a solution. This function is the smallest solution, since if we have another solution \(\tilde{u}\) such that \(0 \le \tilde{u} \le w_0(x)\) then we check sequentially that \(\tilde{u} \ge u_n\), hence in the limit \(\tilde{u} \ge u\). We denote the minimum solution by \(\underline{u}(x)\). This minimum solution is l.s.c. We turn now to the maximum solution. We define a decreasing sequence by starting with the ceiling function and using the same iteration, namely

\(u^0(x) = w_0(x),\)
\(u^{n+1}(x) = \inf_{v \in U} [l(x, v) + \alpha \Phi^v u^n(x)].\)

We have \(u^n(x) \downarrow u(x)\) hence also
\(u^{n+1}(x) \ge \inf_v [l(x, v) + \alpha \Phi^v u(x)].\)

Therefore,
\(u(x) \ge \inf_v [l(x, v) + \alpha \Phi^v u(x)].\)

On the other hand, for any \(v\) we can write the inequality
\(u^{n+1}(x) \le [l(x, v) + \alpha \Phi^v u^n(x)].\)

To pass to the limit we have to be careful that \(u^n(x)\) is decreasing. We cannot use Fatou's Lemma directly. However the sequence \(w_0(x) - u^n(x)\) is increasing and positive. Therefore, applying Fatou's Lemma to this sequence, we can assert that
\(\Phi^v u^n(x) \downarrow \Phi^v u(x).\)

It follows that
\(u(x) \le \inf_v [l(x, v) + \alpha \Phi^v u(x)].\)

and since the reverse inequality is true, the function \(u\) is a solution of equation (4.3.7). One can check easily that it is the maximum solution, within the interval \(0, w_0(x)\). This maximum solution is denoted by \(\overline{u}(x)\). The proof has been completed. \(\square\)

## 4.4. PROBABILISTIC INTERPRETATION

### 4.4.1. THE MINIMUM SOLUTION.
We recall the monotone increasing process

(4.4.1)
\(u_0(x) = 0,\)
\(u_{n+1}(x) = \inf_{v \in U} [l(x, v) + \alpha \Phi^v u_n(x)].\)

The function \(u_n(x)\) is l.s.c. and bounded below. There will exist a Borel function \(\hat{v}_n(x)\) with values in \(U\) such that
\(u_{n+1}(x) = l(x, \hat{v}_n(x)) + \alpha \Phi^{\hat{v}_n(x)} u_n(x).\)

Consider the cost function defined by (4.2.2). Let us define the truncated cost function

\(J_x^n(V) = E^{V,x} \left[ \sum_{j=1}^n \alpha^{j-1} l(y_j, v_j) \right].\)

We define from the feedback introduced above, the control policy

\(\hat{V}_n = (\hat{v}_1, \cdots, \hat{v}_n, \cdots),\)

where

$$\begin{aligned} \hat{v}_{jn}(x_1, \cdots, x_j) &= \hat{v}_j(x_j), \forall 1 \le j \le n, \\ \hat{v}_{jn}(x_1, \cdots, x_j) &= \bar{v} \text{ (arbitrary)} \forall j \ge n + 1. \end{aligned}$$

We can state

### Lemma 4.4.
We have the interpretation

$$u_n(x) = \inf_V J_x^n(V) \tag{4.4.2}$$

**PROOF.** Pick any control V. For $j=0, \cdots, n-1$ we can write

$$\begin{aligned} u_{j+1}(y_{n-j}) &\le l(y_{n-j}, v_{n-j}) + \alpha \Phi^{v_{n-j}} u_j(y_{n-j}) \\ &= l(y_{n-j}, v_{n-j}) + \alpha E^{V,x}[u_j(y_{n-j+1}) | Y^{n-j}]. \end{aligned}$$

Hence also

$$E^{V,x} \alpha^{n-j-1} u_{j+1}(y_{n-j}) \le E^{V,x} \alpha^{n-j-1} l(y_{n-j}, v_{n-j}) + E^{V,x} \alpha^{n-j} u_j(y_{n-j+1}).$$

Adding up from $j=0, \cdots, n-1$ we get

$$u_n(x) \le J_x^n(V).$$

Similarly we can check that

$$u_n(x) = J_x^n(\tilde{V}_n),$$

and the result has been obtained.

We can then state

### Theorem 4.4.
Under the assumptions (4.3.1), (4.3.2), (4.3.6) the minimum solution $\underline{u}(x)$ of the functional equation (4.3.7) between 0 and $w_0$ is the value function

$$\underline{u}(x) = \inf_V J_x(V).$$

Moreover there exists an optimal control policy $\hat{V}$.

**PROOF.** For any decision rule V, we have according to Lemma 4.4,

$$u_n(x) \le J_x^n(V) \le J_x(V).$$

Therefore

$$\underline{u}(x) \le J_x(V),$$

and since V is arbitrary

$$\underline{u}(x) \le \inf_V J_x(V).$$

On the other hand, since $\underline{u}(x)$ is l.s.c. positive, there exists a Borel map $\tilde{v}(x)$ such that

$$\underline{u}(x) = l(x, \tilde{v}(x)) + \alpha \Phi^{\tilde{v}} \underline{u}(x).$$

One then defines a control policy $\hat{V}$ as follows

$$\hat{V} = (\hat{v}_1, \cdots, \hat{v}_n, \cdots),$$

where

$$\hat{v}_n(x_1, \cdots, x_n) = \hat{v}_n(x_n).$$

We obtain easily

$$\underline{u}(x) = \sum_{j=1}^n E^{V,x} \alpha^{j-1} l(y_j, \hat{v}_j) + \alpha^n E^{V,x} \underline{u}(y_{n+1}),$$

and since \(\underline{u}(x) \ge 0\) we have

\(\underline{u}(x) \ge \sum_{j=1}^n E^{\hat{V},x} \alpha^{j-1} l(y_j, \hat{v}_j).\)

Letting \(n \to \infty\) yields

\(\underline{u}(x) \ge J_x(\hat{V}),\)

which implies in fact equality. The result has been obtained.

### 4.4.2. THE MAXIMUM SOLUTION.

We turn now to the interpretation of the maximum solution \(\bar{u}(x)\). We begin by interpreting the function \(u^n(x)\) obtained by the decreasing sequence

(4.4.3) \(\begin{aligned} u^0(x) &= w_0(x), \\ u^{n+1}(x) &= \inf_{v \in U} [l(x, v) + \alpha \Phi^v u^n(x)]. \end{aligned}\)

We define a set of control policies as follows

(4.4.4) \(\begin{aligned} \mathcal{V}^n = \{V = (v_1, \cdots, v_j, \cdots) \text{ where} \\ v_j &= v_j(x_1, \cdots, x_j) \forall j \le n, \\ v_j &= v_0 \forall j \ge n+1 \}, \end{aligned}\)

where the functions \(v_j\) are Borel functions with values in \(U\). We then state the

### Lemma 4.5.
We have the interpretation

(4.4.5) \(u^n(x) = \inf_{V \in \mathcal{V}^n} J_x(V)\)

**PROOF.** By a reasoning similar to that of Lemma 4.4 we can write, for an arbitrary control policy \(V\) (not necessarily in \(\mathcal{V}^n\))

\(u^n(x) \le E^{V,x} \sum_{j=1}^n \alpha^{j-1} l(y_j, v_j) + E^{V,x} \alpha^n w_0(y_{n+1}).\)

Take now \(V \in \mathcal{V}^n\). We can write for \(m \ge n\)

\(E^{V,x} [\mathbf{I}_{\Gamma}(y_{m+1}) | y^m) = \Phi^{v_0} \mathbf{I}_{\Gamma}(y_m).\)

Considering next \(w_0\), we can write for \(j \ge n+1\)

\(w_0(y_j) = l(y_j, v_0) + \alpha E^{V,x} [w_0(y_{j+1}) | \mathcal{Y}^j].\)

In particular

\(E^{V,x} w_0(y_{n+1}) = E^{V,x} \sum_{j=n+1}^\infty \alpha^{j-n-1} l(y_j, v_0),\)

hence also

\(u^n(x) \le E^{V,x} \sum_{j=1}^\infty \alpha^{j-1} l(y_j, v_j), \forall V \in \mathcal{V}^n.\)

Next we note that the functions \(u^n(x)\) are l.s.c. hence we can define a Borel map \(v^n(x)\) such that

\(u^n(x) = l(x, v^n(x)) + \alpha \Phi^{v^n(x)} u^n(x).\)

One then defines

\(\hat{V}^n = (\hat{v}_1^n, \cdots, \hat{v}_j^n, \cdots),\)
