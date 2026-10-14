

$t^*, \gamma^*$, $r$, new temporal variable, new production constant, and the retardation factor of the medium respectively.

考虑渗流速度随距离和时间线性变化，并假设弥散系数与渗流速度的平方成正比（Kumar et al., 2009），两者经进一步修正后写为

$$u=u_0f(pt)(a+b^*x)$$  \tag{19.10}

其中，速度由 $x=0$ 处的 $f(pt)au_0$ 增加到 $x=L$ 处的 $f(pt)(a+e)u_0$，使得 $b^*=\frac{e}{L}$ 为介质的不均匀性参数；为保证达西定律的有效性（即介质中速度的变化不应过大），假设当 $x\to\infty$ 时，$b^*x\to M$，其中 $b^*=\frac{M}{x}$。利用式 (19.10)，弥散系数写为：

$$D=D_0f^2(pt)(a+b^*x)^2$$  \tag{19.11}

使用变换

$$y=\log(a+b^*x)^2$$  \tag{19.12}

式 (19.6) 变为

$$r\frac{\partial c}{\partial t^*}=\left[4(b^*)^2D_0f(pt)\frac{\partial^2c}{\partial y^2}-2u_0g(pt)\frac{\partial c}{\partial y}-b^*u_0c+\gamma^*\right]$$  \tag{19.13}

其中，$$g(pt)=\left(1-\frac{D_0f(pt)(b^*)}{u_0}\right)$$  \tag{19.14}

现在，采用变换

$$z=\frac{1}{2b^*}\int\frac{g(pt)}{f(pt)}\,dy$$  \tag{19.15}

式 (19.13) 变为

$$r\frac{f(pt)}{g^2(pt)}\frac{\partial c}{\partial t^*}=\left[D_0\frac{\partial^2c}{\partial z^2}-u_0\frac{\partial c}{\partial z}-b^*u_0c\frac{f(pt)}{(g(pt))^2}+\gamma^*\frac{f(pt)}{(g(pt))^2}\right]$$  \tag{19.16}

进一步；将时间变量改为

$$t^{**}=\int_0^t\frac{g^2(pt)}{f(pt)}\,dt^*$$  \tag{19.17}

式 (19.16) 化简为

$$r\frac{\partial c}{\partial t^{**}}=\left[D_0\frac{\partial^2c}{\partial z^2}-u_0\frac{\partial c}{\partial z}-b^*u_0c\frac{f(pt)}{g(pt)^2}+\gamma^*\frac{f(pt)}{g(pt)^2}\right]$$  \tag{19.18}

此外，初始和边界条件 (19.2) 至 (19.4) 变换为

$$c(z,0)=c_i+\left[\frac{1-a\left(1+\frac{D_0}{u_0}b^*\right)b^*z}{b^*}\right]\frac{\gamma^*}{u_0}$$ (19.19)

$$c(0,t^{**})=c_i+c_0(1-\delta t^{**}),\quad t^{**}>0$$ (19.20)

$$\frac{\partial c}{\partial z}=0,\quad z\to\infty$$ (19.21)

为简化起见，采用如下变换 $k(z,t^{**})$：

$$c(z,t^{**})=k(z,t^{**})\exp\left[\frac{u_0}{2D_0}z-\frac{1}{r}\left\{\frac{u_0^2}{4D_0}+\frac{f(pt)u_0}{g^2(pt)}b^*\right\}t^{**}\right]+\frac{\gamma^*}{b^*u_0}$$ (19.22)

因此，式 (19.18) 变换为

$$r\frac{\partial k}{\partial t^{**}}=D_0\frac{\partial^2k}{\partial z^2}+\frac{\gamma^*f(pt)u_0}{g^2(pt)}(1-b^*)k$$ (19.23)

$$r\frac{\partial k}{\partial t^{**}}=D_0\frac{\partial^2k}{\partial z^2}+\phi_1k$$ (19.24)

其中

$$\frac{\gamma^*f(pt)u_0}{g^2(pt)}(1-b^*)=\phi_1$$ (19.25)

式 (19.19) 至 (19.21) 因式 (19.22) 变换如下

$$k(z,0)=c_i e^{-\frac{u_0}{2D_0}z}+\left[\frac{1-a\left(1+\frac{D_0}{u_0}b^*\right)b^*z}{b^*}\right]\frac{\gamma^*}{u_0}e^{-\frac{u_0}{2D_0}z}-\frac{\gamma^*}{b^*u_0}$$ (19.26)

$$k(0,t^{**})=\left[c_i-\frac{\gamma^*}{b^*u_0}+c_0(1-\delta t^{**})\right]\exp(\phi_1t^{**}),\quad t^{**}>0$$ (19.27)

$$\frac{\partial k}{\partial z}=-\frac{ku_0}{2D_0},\quad z\to\infty$$ (19.28)

对式 (19.24) 采用拉普拉斯变换技术，并结合式 (19.26) 至 (19.28)，再变换回初始浓度函数 $c(x,t)$，式 (19.1) 的解析解写为如下：

c(z,t^{**}) = \left[\left(c_i + c_0 - \frac{\gamma^*}{b^* u_0}\right)A(z,t^{**}) - \delta c_0 B(z,t^{**})\right] \exp\left(\frac{u_0}{2D_0}z - \phi t^{**}\right) 
+ \left(-c_i + \frac{a\gamma^*}{b^* u_0}\right)C(z,t^{**})\exp\left(\frac{u_0}{2D_0}z - \phi t^{**}\right) 
+ \frac{a\gamma^*}{r}\left(1 + \frac{D_0 b^*}{u_0}\right)E(z,t^{**})\exp\left(\frac{u_0}{2D_0}z - \phi t^{**}\right) 
+ \left(c_i - a\frac{\gamma^*}{b^* u_0} + a\frac{\gamma^*}{u_0}\left(1 + \frac{D_0 b^*}{u_0}\right)z - \frac{a\gamma^*}{r}\left(1 + \frac{D_0 b^*}{u_0}\right)t^{**}\right)\exp\left(\left(\frac{u_0^2}{4rD_0} - \frac{\phi_1}{r}\right)t^{**}\right)\exp(-\phi t^{**}) 
+ \frac{\gamma^*}{b^* u_0} \tag{19.29}

A(z,t^{**}) = \frac{1}{2}\exp\left(\left(\phi_2 - \frac{\phi_1}{r}\right)t^{**} - \sqrt{\frac{r\phi_2}{D_0}}z\right)erfc\left(\frac{1}{2}\sqrt{\frac{r}{D_0 t^{**}}}z - \sqrt{\phi_2 t^{**}}\right) 
+ \frac{1}{2}\exp\left(\left(\phi_2 - \frac{\phi_1}{r}\right)t^{**} + \sqrt{\frac{r\phi_2}{D_0}}z\right)erfc\left(\frac{1}{2}\sqrt{\frac{r}{D_0 t^{**}}}z + \sqrt{\phi_2 t^{**}}\right) \tag{19.30}

B(z,t^{**}) = \frac{1}{2}\left(t^{**} + \sqrt{\frac{r}{D_0\phi_2}}z\right)\exp\left(\left(\phi_2 - \frac{\phi_1}{r}\right)t^{**} + \sqrt{\frac{r\phi_2}{D_0}}z\right) 
 erfc\left(\frac{1}{2}\sqrt{\frac{r}{D_0 t^{**}}}z + \sqrt{\phi_2 t^{**}}\right) + \frac{1}{2}\left(t^{**} - \sqrt{\frac{r}{D_0\phi_2}}z\right) 
\exp\left(\left(\phi_2 - \frac{\phi_1}{r}\right)t^{**} - \sqrt{\frac{r\phi_2}{D_0}}z\right)erfc\left(\frac{1}{2}\sqrt{\frac{r}{D_0 t^{**}}}z - \sqrt{\phi_2 t^{**}}\right) \tag{19.31}

C(z,t^{**}) = \frac{1}{2}\exp\left(\left(-\frac{\phi_1}{r} + \frac{u_0^2}{4rD_0}\right)t^{**} - \frac{u_0}{2D_0}z\right) 
 erfc\left(\frac{1}{2}\sqrt{\frac{r}{D_0 t^{**}}}z - \frac{u_0}{2}\sqrt{\frac{t^{**}}{D_0 r}}\right) + \frac{1}{2}\exp\left(\left(-\frac{\phi_1}{r} + \frac{u_0^2}{4rD_0}\right)t^{**} + \frac{u_0}{2D_0}z\right) 
 erfc\left(\frac{1}{2}\sqrt{\frac{r}{D_0 t^{**}}}z + \frac{u_0}{2}\sqrt{\frac{t^{**}}{D_0 r}}\right) \tag{19.32}

E(z,t^{**}) = \begin{bmatrix} \frac{1}{2}\left(t^{**} + \frac{r z}{u_0}\right)\exp\left(\frac{u_0^2}{4rD_0}t^{**} + \frac{u_0}{2D_0}z - \frac{\phi_1}{r}t^{**}\right)erfc\left(\frac{1}{2}\sqrt{\frac{r}{D_0 t^{**}}}z + \frac{u_0}{2\sqrt{rD_0}}\sqrt{t^{**}}\right) + \\
 \frac{1}{2}\left(t^{**} - \frac{r z}{u_0}\right)\exp\left(\frac{u_0^2}{4rD_0}t^{**} - \frac{u_0}{2D_0}z - \frac{\phi_1}{r}t^{**}\right)erfc\left(\frac{1}{2}\sqrt{\frac{r}{D_0 t^{**}}}z - \frac{u_0}{2\sqrt{rD_0}}\sqrt{t^{**}}\right) \end{bmatrix} \tag{19.33}

其中，$\phi = \frac{1}{r}\left\{\frac{u_0^2}{4D_0} + \frac{f(pt)u_0}{g^2(pt)}b^*\right\}$  (19.34)

$\phi_2 = \phi + \frac{\phi_1}{r}$  (19.35)

式 (19.1) 也对柯西型边界条件求解。由于人类对地表/地下表面的干扰不断增加，污染水平持续增长；该情况由第三类或柯西型边界条件适当模拟。在原点，混合型边界条件的数学形式为：

$-D\frac{\partial c}{\partial x} + uc = u\left(c_i + c_0 e^{-\delta t}\right); x=0, t>0$  (19.36)

通过拉普拉斯变换技术求解式 (19.24)，解为

$c(z,t^{**}) = \frac{-2D_0}{qu_0}\left[\begin{array}{c}\left(c_i + c_0 - \frac{\gamma^*}{b^*u_0}\right)A(z,t^{**})\\ -\delta c_0 B(z,t^{**})\end{array}\right] \exp\left(\frac{u_0}{2D_0}z - \phi t^{**}\right) - \frac{2D_0}{qu_0}\left(\frac{qa\gamma^* b^*}{r}\left(1 + \frac{D_0 b^*}{u_0}\right) + \left(-c_i + \frac{a\gamma^*}{b^*u_0}\right)\right) E(z,t^{**})\exp\left(\frac{u_0}{2D_0}z - \phi t^{**}\right) - \frac{4D_0\sqrt{rD_0}}{qu_0^2}\left(\left(c_i + c_0 - \frac{\gamma^*}{b^*u_0}\right)A_1(z,t^{**}) - \delta c_0 B_1(z,t^{**})\right)\exp\left(\frac{u_0}{2D_0}z - \phi t^{**}\right) + \left(-\frac{a\gamma^*}{r}\left(1 + \frac{D_0 b^*}{u_0}\right)t^{**}\right)\exp\left(\frac{u_0^2}{4rD_0} - \frac{\phi_1}{r}\right)t^{**}\exp\left(-\frac{u_0}{2D_0}z\right)\exp\left(\frac{u_0}{2D_0}z - \phi t^{**}\right) + \left(c_i - a\frac{\gamma^*}{b^*u_0} + a\frac{\gamma^*}{u_0}\left(1 + \frac{D_0 b^*}{u_0}\right)z\right)\exp\left(\frac{u_0^2}{4rD_0} - \frac{\phi_1}{r}\right)t^{**}\exp\left(-\frac{u_0}{2D_0}z\right)\exp\left(\frac{u_0}{2D_0}z - \phi t^{**}\right) + \frac{\gamma^*}{b^*u_0}$  (19.37)

$B(z,t^{**}) = \frac{1}{2}\left(t^{**} + \sqrt{\frac{r}{D_0\phi_2}}z\right)\exp\left(\left(\phi_2 - \frac{\phi_1}{r}\right)t^{**} + \sqrt{\frac{r\phi_2}{D_0}}z\right) erfc\left(\frac{1}{2}\sqrt{\frac{r}{D_0 t^{**}}}z + \sqrt{\phi_2 t^{**}}\right) + \frac{1}{2}\left(t^{**} - \sqrt{\frac{r}{D_0\phi_2}}z\right)$

