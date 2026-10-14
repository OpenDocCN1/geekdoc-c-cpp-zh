
等等。

## 定理 22.2. 拉盖尔分数阶多项式的正交性。

$$\int_{0}^{\infty} e^{-x^{\beta}} x^{\beta-1} L_{n}(x^{\beta}) L_{m}(x^{\beta}) dx = \frac{1}{\beta} \delta_{mn} \begin{cases}0, m \neq n \\ 1, m = n\end{cases}$$

**证明.** 考虑

$$\sum_{n=0}^{\infty} L_{n}(x^{\beta}) t^{n} = \frac{\exp\left(\frac{-x^{\beta} t}{1-t}\right)}{1-t} \quad \text{与} \quad \sum_{m=0}^{\infty} L_{m}(x^{\beta}) s^{m} = \frac{\exp\left(\frac{-x^{\beta} s}{1-s}\right)}{1-s}$$

$$\sum_{n=0}^{\infty} \sum_{m=0}^{\infty} L_{n}(x^{\beta}) L_{m}(x^{\beta}) t^{n} s^{m} = \frac{\exp\left(\frac{-x^{\beta} t}{1-t} + \frac{-x^{\beta} s}{1-s}\right)}{(1-t)(1-s)}$$

两边乘以 $x^{\beta-1} e^{-x^{\beta}}$ 并积分

$$\sum_{n=0}^{\infty} \sum_{m=0}^{\infty} \int_{0}^{\infty} e^{-x^{\beta}} x^{\beta-1} L_{n}(x^{\beta}) L_{m}(x^{\beta}) t^{n} s^{m} dx = \frac{1}{(1-t)(1-s)} \int_{0}^{\infty} \exp\left(-x^{\beta} + \frac{-x^{\beta} t}{1-t} + \frac{-x^{\beta} s}{1-s}\right) dx$$

$$= \frac{1}{\beta (1-t)(1-s)} \left[ \frac{e^{-x^{\beta} \{1+t/(1-t)+s/(1-s)\}}}{\{1+t/(1-t)+s/(1-s)\}} \right]_{\infty}^{0}$$

$$= \frac{1}{\beta (1 - s t)}$$

$$= \frac{1}{\beta} \sum_{n=0}^{\infty} t^{n} s^{n}$$

现在比较两边 $t^{n} s^{n}$ 的系数，我们得到

$$\int_{0}^{\infty} e^{-x^{\beta}} x^{\beta-1} L_{n}(x^{\beta}) L_{m}(x^{\beta}) dx = 0, \; m \neq n$$

$$\int_{0}^{\infty} e^{-x^{\beta}} x^{\beta-1} L_{n}(x^{\beta}) L_{m}(x^{\beta}) dx = \frac{1}{\beta}, \; m = n$$

## 定理 22.3. $L_{n}(x^{\beta})$ 具有以下递推关系：

- (a) $(n+1)L_{n+1}(x^{\beta}) = (2n+1 - x^{\beta}) L_{n}(x^{\beta}) - n L_{n-1}(x^{\beta})$
- (b) $L'_{n+1}(x^{\beta}) = L'_{n}(x^{\beta}) - L_{n}(x^{\beta})$
- (c) $x^{\beta} L'_{n}(x^{\beta}) = n L_{n}(x^{\beta}) - n L_{n-1}(x^{\beta})$

**证明.** (a) 我们有

$$\sum_{n=0}^{\infty} L_n(x^{\beta}) t^n = \frac{1}{1-t} e^{-\frac{x^{\beta} t}{1-t}}$$

关于 $t$ 求导

$$\sum_{n=0}^{\infty} n L_n(x^{\beta}) t^{n-1} = \frac{1}{(1-t)^2} e^{-\frac{x^{\beta} t}{1-t}} - \frac{x^{\beta}}{(1-t)^3} e^{-\frac{x^{\beta} t}{1-t}}$$

$$= \frac{1}{1-t} \sum_{n=0}^{\infty} L_n(x^{\beta}) t^n - \frac{x^{\beta}}{(1-t)^2} \sum_{n=0}^{\infty} L_n(x^{\beta}) t^n$$

$$(1 - 2t + t^2) \sum_{n=0}^{\infty} n L_n(x^{\beta}) t^{n-1} = (1-t)\sum_{n=0}^{\infty} L_n(x^{\beta}) t^n - x^{\beta} \sum_{n=0}^{\infty} L_n(x^{\beta}) t^n$$

比较两边 $t^n$ 的系数

$$(n+1)L_{n+1}(x^{\beta}) = (2n+1 - x^{\beta}) L_n(x^{\beta}) - n L_{n-1}(x^{\beta})$$

(b) 在生成函数的定义中对两边施加 $x^\beta$ 导数

$$\sum_{n=0}^{\infty} L'_n(x^{\beta}) t^n = -\frac{t}{(1-t)^2} e^{-\frac{x^{\beta} t}{1-t}},$$

这意味着

$$(1-t) \sum_{n=0}^{\infty} L'_n(x^{\beta}) t^n = -t \sum_{n=0}^{\infty} L_n(x^{\beta}) t^n$$

比较 $t^{n+1}$ 的系数

$$L'_{n+1}(x^{\beta}) = L'_n(x^{\beta}) - L_n(x^{\beta})$$

以及

(c) $x^\beta L'_n(x^\beta) = n L_n(x^\beta) - n L_{n-1}(x^\beta)$ 由 (a) 和 (b) 得出。

## 22.3 合意分数阶切比雪夫方程及其解

$$(1 - x^{2\beta}) D^{2\beta} y - \beta x^\beta D^\beta y + \beta^2 p^2 y = 0$$

其中 $x > 0$，$p$ 是实常数。

我们感兴趣的是在常点 $x = 0$ 附近求级数解，因此考虑 $y = \sum_{r=0}^{\infty} c_r x^{r\beta}$
于是根据合意导数的定义，有 $D^{\beta}y=\sum_{r=0}^{\infty}\beta r c_r x^{(r-1)\beta}$ 和 $D^{2\beta}y=\sum_{r=0}^{\infty}\beta r(r-1)c_r x^{(r-2)\beta}$。

$$\Rightarrow \sum_{r=2}^{\infty}\beta^2r(r-1)c_rx^{(r-2)\beta}-\sum_{r=2}^{\infty}\beta^2r(r-1)c_rx^{r\beta}-\sum_{r=1}^{\infty}\beta^2rc_rx^{r\beta}+p^2\sum_{r=0}^{\infty}\beta^2c_rx^{r\beta}=0$$

$$\Rightarrow \sum_{r=2}^{\infty}r(r-1)c_rx^{(r-2)\beta}-\sum_{r=2}^{\infty}r(r-1)c_rx^{r\beta}-\sum_{r=1}^{\infty}rc_rx^{r\beta}+p^2\sum_{r=0}^{\infty}c_rx^{r\beta}=0$$

$$\Rightarrow 2c_2+p^2c_0+(6c_3-c_1+p^2c_1)x^\beta+\sum_{r=0}^{\infty}\left[(r+2)(r+1)c_{r+2}-\{r(r-1)+r-p^2\}c_r\right]x^{r\beta}=0$$

将常数项和 $x^{\beta r}$ 的系数设为零，我们得到

$$2c_2+p^2c_0=0\Rightarrow c_2=-\frac{p^2}{2}c_0,\ldots,c_{r+2}=\frac{r^2-p^2}{(r+1)(r+2)}c_r$$

令 $r=1,2,3...$ 我们得到

$$c_3=\frac{1-p^2}{3!}c_1,\quad c_4=\frac{(2^2-p^2)(-p^2)}{4!}c_0,\quad c_5=\frac{(3^2-p^2)(1-p^2)}{5!}c_1,\quad c_6=\frac{(4^2-p^2)(2^2-p^2)(-p^2)}{6!}c_0$$

一般地

$$c_{2r}=\frac{[(2r-2)^2-p^2][(2r-4)^2-p^2]\cdots[2^2-p^2](-p^2)}{(2r)!}c_0$$

$$c_{2r+1}=\frac{[(2r-1)^2-p^2][(2r-3)^2-p^2]\cdots(3^2-p^2)(1^2-p^2)}{(2r+1)!}c_1$$

因此完整解为

$$y=A\left(1+\sum_{r=1}^{\infty}\frac{[(2r-2)^2-p^2][(2r-4)^2-p^2]\cdots[2^2-p^2](-p^2)}{(2r)!}x^{2r\beta}\right)+B\left(x+\sum_{r=1}^{\infty}\frac{[(2r-1)^2-p^2][(2r-3)^2-p^2]\cdots(3^2-p^2)(1^2-p^2)}{(2r+1)!}x^{(2r+1)\beta}\right)$$

其中 $A,B$ 为常数。

## 22.3.1 合意分数阶切比雪夫微分方程的另一种形式

$$(1-x^{2\beta})D^{\beta}D^{\beta}y-\beta x^{\beta}D^{\beta}y+\beta^2p^2y=0$$

利用变换 $x^{\beta}=\cos t$；$D^{\beta} y = \frac{d^{\beta} y}{dx^{\beta}} = \frac{-\beta}{\sqrt{1-x^{2\beta}}} \frac{d^{\beta} y}{dt^{\beta}}$ 以及

$$D^{\beta} D^{\beta} y = \frac{d^{\beta}}{dx^{\beta}}\left(\frac{-\beta}{\sqrt{1-x^{2\beta}}}\frac{d^{\beta} y}{dt^{\beta}}\right)=\frac{-\beta^{2}x^{\beta}}{(1-x^{2\beta})^{3/2}}\frac{d^{\beta} y}{dt^{\beta}}-\frac{\beta}{\sqrt{1-x^{2\beta}}}\frac{d^{\beta}}{dt^{\beta}}\frac{d^{\beta} y}{dt^{\beta}}$$

将所有导数的值代入，我们得到

$$\frac{d^{\beta}}{dt^{\beta}}\frac{d^{\beta} y}{dt^{\beta}}+p^{2}y=0$$

其解为 $y = c_{1}\cos\left(\frac{p}{\beta}\cos^{-1}x^{\beta}\right)+c_{2}\sin\left(\frac{p}{\beta}\cos^{-1}x^{\beta}\right)$，或等价地

$$y(x^{\beta}) = c_{1}U_{p}(x^{\beta})+c_{2}V_{p}(x^{\beta})$$

其中 $U_{p}$ 和 $V_{p}$ 分别定义为 $x^{\beta}$ 的第一类和第二类切比雪夫分数阶多项式。

对于 $0 < x^{\beta} < 1$，$U_{p}(x^{\beta}) \pm i V_{p}(x^{\beta}) = (\cos t \pm i \sin t)^{p} = (x^{\beta} \pm i\sqrt{1-x^{2\beta}})^{p}$

因此 $U_{p}(x^{\beta}) = \frac{1}{2}\left[\left(x^{\beta}+i\sqrt{1-x^{2\beta}}\right)^{p}+\left(x^{\beta}-i\sqrt{1-x^{2\beta}}\right)^{p}\right]$ 以及

$$V_{p}(x^{\beta}) = \frac{1}{2i}\left[\left(x^{\beta}+i\sqrt{1-x^{2\beta}}\right)^{p}-\left(x^{\beta}-i\sqrt{1-x^{2\beta}}\right)^{p}\right]$$

## 22.3.2 切比雪夫分数阶多项式的罗德里格斯公式

$$U_{p}(x^{\beta}) = \frac{(-2)^{p}p!}{(2p)!\beta^{p}}\sqrt{1-x^{2\beta}}\frac{d^{\beta}}{dx^{\beta}}\left(1-x^{2\beta}\right)^{p-1/2}$$

将 $p = 0,1,2,3...$ 代入，可以得到第一类切比雪夫分数阶多项式：

$$U_{0}(x^{\beta}) = 1$$

$$U_{1}(x^{\beta}) = x^{\beta}$$

$$U_{2}(x^{\beta}) = 2x^{2\beta} - 1$$

$$U_{3}(x^{\beta}) = 4x^{3\beta} - 3x^{\beta}$$

$$U_{4}(x^{\beta}) = 8x^{4\beta} - 8x^{2\beta} + 1$$

等等。

## 22.3.3 $U_n(x^\beta)$ 的生成函数

第一类切比雪夫分数阶多项式可由下式展开：

$$\frac{1 - t x^\beta}{1 - 2 t x^\beta + t^2} = \sum_{n=0}^{\infty} U_n(x^\beta) t^n$$

## 22.4 结论

我们讨论了合意分数阶拉盖尔和切比雪夫微分方程的分数阶幂级数解以及相应的函数。这项工作表明，当 $\beta=1$ 时，所有的解和函数都表现为经典函数。此外，我们还给出了这些特殊分数阶函数的一些性质。整个工作的结果表明，分数阶情形的结果与普通情形的结果是一致的。

## 致谢

作者感谢审稿人对改进稿件所提出的宝贵而富有建设性的建议。同时，我们也要感谢所有在本工作完成过程中直接或间接给予合作的人员。

## 参考文献

- 1. Podlubny, Igor. *Fractional Differential Equations: An Introduction to Fractional Derivatives, Fractional Differential Equations, to Methods of Their Solution and Some of Their Applications.* Vol. 198.
- 2. Kilbas A., Anatolii Aleksandrovich, Hari Mohan Srivastava, and Juan J. Trujillo. *Theory and Applications of Fractional Differential Equations.* Vol. 204, 2006.
- 3. Debnath, Lokenath. “A brief historical introduction to fractional calculus.” *International Journal of Mathematical Education in Science and Technology* 35, no. 4 (2004): 487–501. doi:10.1080/00207390410001686571
- 4. Tomovski, Živorad, Rudolf Hilfer, and H. M. Srivastava. “Fractional and operational calculus with generalized fractional derivative operators and Mittag–Leffler type functions.” *Integral Transforms and Special Functions* 21, no. 11 (2010): 797–814. doi:10.1080/10652461003675737
- 5. Khalil, Roshdi, Mohammed Al Horani, Abdelrahman Yousef, and Mohammad Sababheh. “A new definition of fractional derivative.” *Journal of Computational and Applied Mathematics* 264 (2014): 65–70. doi:10.1016/j.cam.2014.01.002
- 6. Atangana, Abdon, Dumitru Baleanu, and Ahmed Alsaedi. “New properties of conformable derivative.” *Open Mathematics* 13, no. 1 (2015).

