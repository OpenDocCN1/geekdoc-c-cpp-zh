It is known from classical electrodynamics that the electric potential $U(x)$ arising from static charges satisfies Poisson’s PDE (Jackson, 1988):

$$\nabla^2 U(x)=-4\pi\rho(x),\tag{19.3}$$

where $\rho(x)$ is the charge density. In charge-free regions of space, that is, regions where $\rho(x)=0$, the potential satisfies *Laplace’s equation*:

$$\nabla^2 U(x)=0.\tag{19.4}$$

Both these equations are elliptic PDEs of a form that occurs in various applications. We solve them in 2D rectangular coordinates:

$$\frac{\partial^2U(x,y)}{\partial x^2}+\frac{\partial^2U(x,y)}{\partial y^2}=0,\qquad \text{Laplace’s equation},\tag{19.5}$$

$$\frac{\partial^2U(x,y)}{\partial x^2}+\frac{\partial^2U(x,y)}{\partial y^2}=-4\pi\rho(x),\qquad \text{Poisson’s equation}.\tag{19.6}$$

In both cases, we see that the potential depends simultaneously on $x$ and $y$. For Laplace’s equation, the charges, which are the source of the field, enter indirectly by specifying the potential values in some region of space; for Poisson’s equation they enter directly.

# 19.3  
Fourier Series Solution of a PDE

For the simple geometry of Figure 19.1, an analytic solution of Laplace’s equation (19.5) exists in the form of an infinite series. If we assume that the solution is the product of independent functions of $x$ and $y$ and substitute the product into (19.5), we obtain

$$U(x,y)=X(x)Y(y)\quad\Rightarrow\quad \frac{d^2X(x)/dx^2}{X(x)}+\frac{d^2Y(y)/dy^2}{Y(y)}=0.\tag{19.7}$$

Because $X(x)$ is a function of only $x$, and $Y(y)$ is a function of only $y$, the derivatives in (19.7) are *ordinary* as opposed to *partial* derivatives. Because $X(x)$ and $Y(y)$ are assumed to be independent, the only way (19.7) can be valid for *all* values of $x$ and $y$ is for each term in (19.7) to be equal to a constant:

$$\frac{d^2Y(y)/dy^2}{Y(y)}=-\frac{d^2X(x)/dx^2}{X(x)}=k^2\tag{19.8}$$

$$\Rightarrow\quad \frac{d^2X(x)}{dx^2}+k^2X(x)=0,\qquad \frac{d^2Y(y)}{dy^2}-k^2Y(y)=0.\tag{19.9}$$

We shall see that this choice of sign for the constant matches the boundary conditions and gives us periodic behavior in $x$. The other choice of sign would give periodic behavior in $y$, and that would not work with these boundary conditions.