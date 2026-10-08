Matrix representation. Algebraic circle fits are based on the algebraic equation of a circle

$A(x^2+y^2)+B x+C y+D=0, \qquad\qquad\qquad\qquad\qquad\qquad\qquad\qquad\qquad\qquad\qquad\qquad (5.61)$

where $\mathbf{A}=(A, B, C, D)^{T}$ is the 4-parameter vector. Every algebraic fit minimizes the function

$\begin{aligned} \mathscr{F}(A, B, C, D) & =\frac{1}{n} \sum_{i=1}^{n}\left(A z_{i}+B x_{i}+C y_{i}+D\right)^{2} \\ & =n^{-1} \mathbf{A}^{T}\left(\mathbf{X}^{T} \mathbf{X}\right) \mathbf{A}=\mathbf{A}^{T} \mathbf{M A}, \end{aligned} \qquad\qquad\qquad\qquad\qquad\qquad\qquad\qquad\qquad\qquad\qquad\qquad (5.62)$

subject to a constraint

$\mathbf{A}^{T} \mathbf{N A}=1 \qquad\qquad\qquad\qquad\qquad\qquad\qquad\qquad\qquad\qquad\qquad\qquad\qquad\qquad\qquad\qquad\qquad\qquad\qquad\qquad\qquad\qquad (5.63)$

for some matrix $\mathbf{N}$. Here we use our shorthand notation $z_{i}=x_{i}^{2}+y_{i}^{2}$ and

$\mathbf{M}=\frac{1}{n} \mathbf{X}^{T} \mathbf{X}=\left[\begin{array}{cccc} \bar{z z} & \bar{z x} & \bar{z y} & \bar{z} \\ \bar{z x} & \bar{x x} & \bar{x y} & \bar{x} \\ \bar{z y} & \bar{x y} & \bar{y y} & \bar{y} \\ \bar{z} & \bar{x} & \bar{y} & 1 \end{array}\right] \text {,} \text { } \qquad\qquad\qquad\qquad\qquad\qquad\qquad\qquad\qquad\qquad\qquad\qquad\qquad\qquad\qquad\qquad\qquad\qquad\qquad\qquad\qquad\qquad (5.64)$

where

$\mathbf{X}=\left[\begin{array}{cccc} z_{1} & x_{1} & y_{1} & 1 \\ \vdots & \vdots & \vdots & \vdots \\ z_{n} & x_{n} & y_{n} & 1 \end{array}\right] \text { . } \qquad\qquad\qquad\qquad\qquad\qquad\qquad\qquad\qquad\qquad\qquad\qquad\qquad\qquad\qquad\qquad\qquad\qquad\qquad\qquad\qquad\qquad (5.64)$

The constraint matrix $\mathbf{N}$ in (5.63) determines the particular algebraic fit. As we know,

$\mathbf{N}=\mathbf{K}=\left[\begin{array}{cccc} 1 & 0 & 0 & 0 \\ 0 & 0 & 0 & 0 \\ 0 & 0 & 0 & 0 \\ 0 & 0 & 0 & 0 \end{array}\right] \qquad\qquad\qquad\qquad\qquad\qquad\qquad\qquad\qquad\qquad\qquad\qquad\qquad\qquad\qquad\qquad\qquad\qquad\qquad\qquad\qquad\qquad (5.65)$

for the Kásá fit, cf. (5.39),

$\mathbf{N}=\mathbf{P}=\left[\begin{array}{cccc} 0 & 0 & 0 & -2 \\ 0 & 1 & 0 & 0 \\ 0 & 0 & 1 & 0 \\ -2 & 0 & 0 & 0 \end{array}\right] \qquad\qquad\qquad\qquad\qquad\qquad\qquad\qquad\qquad\qquad\qquad\qquad\qquad\qquad\qquad\qquad\qquad\qquad\qquad\qquad\qquad\qquad (5.66)$

for the Pratt fit, see (5.27), and

$\mathbf{N}=\mathbf{T}=\left[\begin{array}{cccc} 4 \bar{z} & 2 \bar{x} & 2 \bar{y} & 0 \\ 2 \bar{x} & 1 & 0 & 0 \\ 2 \bar{y} & 0 & 1 & 0 \\ 0 & 0 & 0 & 0 \end{array}\right] \text {, } \qquad\qquad\qquad\qquad\qquad\qquad\qquad\qquad\qquad\qquad\qquad\qquad\qquad\qquad\qquad\qquad\qquad\qquad\qquad\qquad\qquad\qquad (5.67)$