![](bbox=[0.111, 0.094, 0.757, 0.224])

# **FIGURE 6.8**

1-closure for 1-map.
(a) A 1-map $M$ with 1-boundary.
(b) The 1-map $M_{1}$-close. Dart 4 is new.

+   2. $\forall j \in \{2,\ldots,n\}$:
+   
+   - $\forall d \in D$, $\beta_j''(d)=\beta_j(d)$;
+   - $\forall d' \in D'$, $\beta_j''(f(d'))=f(\beta_j'(d'))$.
+   
+   3. $\forall d \in D \setminus D'$, $\beta_1''(d)=\beta_1(d)$;
+   
+   4. $\forall d' \in D'$, $\beta_1''(d')=f(d)$, $\beta_1''(f(d))=\beta_0^k(d)$,
+   
+   where $k$ is the smaller positive integer s.t. $\beta_0^k(d)$ is 0-free.

There are two differences with the definition of the $i$-closure for $i \geq 2$. First, the 1-boundary map $M_{\partial_1}$ is considered and not its inverse. Indeed, all darts in $D'$ are 1-free, thus $M_{\partial_1}=M_{\partial_1}^{-1}$. Second, $\beta_1''(f(d))$ is not equal to $d$, since $\beta_1$ is not an involution. It is equal to $\beta_0^k(d)$, $k$ being the smaller positive integer such that $\beta_0^k(d)$ is 0-free. Intuitively, $\beta_1$ defines polygonal lines, and $\beta_0$ is the second extremity of the open polygonal line incident to $d$.

The 1-closure operation is illustrated in Fig. 6.8. Starting from the 1-map with boundary depicted in (a), the 1-map without boundary shown in (b) is obtained by applying the 1-closure operation. In the initial 1-map, there is one 1-free dart (numbered 3), thus one dart (numbered 4) is created. $\beta_1''(3)=f(3)=4$, since dart 4 is the new dart corresponding to dart 3. However, it is more complex to define $\beta_1''(4)$, since it is necessary to retrieve the 0-free dart belonging to the same polygonal line. So, $\beta_0^k(3)$ has to be computed, where $k$ is the smaller positive integer such that $\beta_0^k(3)$ is 0-free. Thus $\beta_1''(4)=\beta_0^2(3)=1$.

Another example of the 1-closure operation is presented in Fig. 6.9, but here for a 3-map. There are two 1-free darts numbered 3 and 4, thus two new darts (numbered 7 and 8) are created. As darts 3 and 4 are 3-sewn in the 1-boundary map $M_{\partial_1}$, the corresponding darts 7 and 8 are also 3-sewn in $M_1$-close: $\beta_1''(3)=f(3)=7$, since dart 7 corresponds to the 1-free dart 3 (similarly, $\beta_1''(4)=8$), and $\beta_1''(7)=\beta_0^3(3)=1$ (similarly, $\beta_1''(8)=\beta_0^2(4)=2$).