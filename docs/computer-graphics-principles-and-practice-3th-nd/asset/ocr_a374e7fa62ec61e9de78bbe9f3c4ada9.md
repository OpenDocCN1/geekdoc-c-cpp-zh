# 30.3.6 Application to the Sphere

Let’s apply the ideas of the previous section to the longitude-colatitude parameterization of $S^2$, namely,

$Y:[0,1]\times[0,1]\to S^2:(u,v)\mapsto(\cos(2\pi u)\sin(\pi v),\cos(\pi v),\sin(2\pi u)\sin(\pi v))$. (30.35)

We’ll start with the uniform probability density $p$ on $[0,1]\times[0,1]$, or $p(u,v)=1$ for all $u,v$. For notational convenience, we’ll write $(x,y,z)=Y(u,v)$. We have the intuitive sense that if we pick points uniformly randomly in the unit square and use $f$ to convert them to points on the unit sphere, they’ll be clustered near the poles. (If you doubt this, you should write a little program to verify it.) This means that the induced probability density on $T$ will not be uniform.

The preceding section shows that

$p_Y(x,y,z)=\dfrac{1}{|Y'(u,v)|}p(u,v)$ (30.36)

$=\dfrac{1}{|Y'(u,v)|}$. (30.37)

![](bbox=[0.707, 0.162, 0.933, 0.466])

But the change-of-area factor (see Figure 30.9) for $Y$ (which is slightly messy to compute) turns out to be

$|Y'(u,v)|=2\pi^2|\sin(\pi v)|$ (30.38)

$=2\pi^2\sqrt{1-\cos^2(\pi v)}$ (30.39)

$=2\pi^2\sqrt{1-y^2}$. (30.40)

And hence,

$p_Y(x,y,z)=\dfrac{1}{2\pi^2\sqrt{1-y^2}}$. (30.41)

Thus, the probability of sampling a point in a small disk of area $A$ centered on the sphere point $(x,y,z)$ is approximately $A/(2\pi^2\sqrt{1-y^2})$.

Figure 30.9: A small area $A$ in the domain of the spherical parameterization gets multiplied by $2\pi^2\sin(\pi v)$.

# 30.3.7 A Simple Example

If we start with the uniformly distributed random variable $U$ on $[0,1]\times[0,1]$ and want a uniformly distributed variable $V$ on, say, $[0,2\pi]\times[0,1]$, it seems obvious to define $V(a,b)=U\left(\dfrac{a}{2\pi},b\right)$. The density for $U$ is the function

$p_U:[0,1]\times[0,1]\to\mathbb{R}:(x,y)\mapsto1$. (30.42)

That makes the density for $V$ be the function

$p_V:[0,2\pi]\times[0,1]\to\mathbb{R}:(x,y)\mapsto\dfrac{1}{2\pi}$. (30.43)

(Quick proof: $V$ is evidently uniformly distributed, and hence its pdf is a constant. The integral of that constant over the domain must be 1, so the constant is $\dfrac{1}{2\pi}$.)