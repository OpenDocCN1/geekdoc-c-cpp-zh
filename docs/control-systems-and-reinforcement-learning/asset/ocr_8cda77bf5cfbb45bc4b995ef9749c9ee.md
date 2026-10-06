# 4.9 Convergence Theory for QSA

The Lipschitz conditions in (QSA2) imply the bound:

$$\|\mathcal{E}_v^{	au+v}\| \leq \delta^	au + L_f \int_{	au}^{	au+v} \|\mathcal{E}_w^	au\| dw,$

where

$$\delta^	au \frac{\text{def}}{=} \sup_{\tau \geq 0 < v < \tau} \int_{	au}^{	au+v} |f(\mathbf{\Theta}_w) - f(\mathbf{\Theta}_w, \xi(s^{-1}(w)))| dw.$

Proposition 4.2 gives $|\mathcal{E}_v^{	au+v}\| \leq e^{l/\tau}$ for all $	au$, and all $0 \leq v \leq 1$. The error term $\delta^	au$ vanishes as $\tau \to \infty$ (4.132a).

# Local Solidarity

We conclude this subsection with a weak but general bound on the difference between $\mathbf{\Theta}$ and $\mathbf{\Theta}^	au$. The inequality does not require boundedness of solutions to the ODEs and is useful for small $T$ to establish a Lyapunov drift condition for $\mathbf{\Theta}$.

**Lemma 4.31** for $b < 0$ and any $0 < T \leq 1$.

$$\|\mathbf{\Theta}_{	au+T} - \mathbf{\Theta}^	au\| \leq e^{l/\tau}b_0(\tau) + b(1 + |\mathbf{\Theta}_	au\|)T^2, \quad (4.136)$

where $b_0(\tau)$ is given in (4.82), and $L_f$ is the Lipschitz constant introduced in Assumption (QSA2).

*Proof* Denote $\mathcal{E}_w^	au = \mathbf{\Theta}_w - \mathbf{\Theta}^	au$ for $w \geq \tau$. The property of (4.131) give

$$\mathcal{E}_{	au+T} = \int_{	au}^{	au+T} [f(\mathbf{\Theta}_w) - f(\mathbf{\Theta}_w, \xi(s^{-1}(w)))] dw + \int_{	au}^{	au+T} [f(\mathbf{\Theta}_w^	au) - f(\mathbf{\Theta}_w)] dw, \quad (4.137)$

The Lipschitz conditions in (QSA2) are used to bound the:

$$\|f(\mathbf{\Theta}_w) - f(\mathbf{\Theta}_	au)\| \leq L_f|\mathbf{\Theta}_w - \mathbf{\Theta}_	au\|,$

$$\|f(\mathbf{\Theta}_w, \xi(s^{-1}(w))) - f(\mathbf{\Theta}_	au, \xi(s^{-1}(w)))\| \leq L_f|\mathbf{\Theta}_w - \mathbf{\Theta}_	au\|,$

$$\|f(\mathbf{\Theta}_w^	au) - f(\mathbf{\Theta}_w)\| \leq L_f|\mathcal{E}_w^	au\|.$

Consequently for $T \geq 0$,

$$\|\mathcal{E}_{	au+T}^	au\| \leq \int_{	au}^{	au+T} [f(\mathbf{\Theta}_w) - f(\mathbf{\Theta}_w, \xi(s^{-1}(w)))] dw \+ 2L_f \int_{	au}^{	au+T} |\mathbf{\Theta}_w - \mathbf{\Theta}_	au\| dw + \int_{	au}^{	au+T} |\mathcal{E}_w^	au| dw$$

$$\leq e^{l/\tau} + L_f \int_{	au}^{	au+T} |\mathcal{E}_w^	au| dw, \quad \delta^	au \frac{\text{def}}{=} b_0(\tau)\mathcal{E}_	au^	au + 2L_f |\mathbf{\Theta}_{	au+w} - \mathbf{\Theta}_	au| dw.$

By Grönwall's lemma, in the form (4.6c),

$$\|\mathcal{E}_{	au+T}^	au\| \leq |\mathcal{E}_	au^	au|e^{L_f T}.$

Using the same proof to derive (4.108b) by Grönwall's lemma, we have

$$\|\mathbf{\Theta}_{	au+w} - \mathbf{\Theta}_	au\| \leq (B_f + L_f|\mathbf{\Theta}_	au\|)e^{L_f w}.