The max product composition can be computed as follows:

$\bar{R}_1 \circ \bar{R}_2(x_1,z_1)=\max\{(1*0.1),(0.4*0.9),(0.5*0)\}$  
$\qquad =\max\{0.1,0.36,0\}=0.36$

$\bar{R}_1 \circ \bar{R}_2(x_1,z_2)=\max\{(1*0.5),(0.4*0.4),(0.5*0.16),0.4\}=0.5$  
$\qquad =\max\{0.5,0.16,0.4\}=0.5$

$\bar{R}_1 \circ \bar{R}_2(x_2,z_1)=\max\{(0.3*0.1),(0*0.9),(0.7*0)\}$  
$\qquad =\max\{0.03,0,0\}=0.03$

$\bar{R}_1 \circ \bar{R}_2(x_2,z_2)=\max\{(0.3*0.1),(0*0.9),(0.7*0)\}$  
$\qquad =\max\{0.03,0,0\}=0.03$

$R_1R_2(x_3,z_1)=\max\{(0.2*0.1),(0.6*0.9),(0.9*0)\}$  
$\qquad =\max\{0.02,0.54,0\}=0.54$

$\bar{R}_1 \circ \bar{R}_2(x_3,z_2)=\max\{(0.2*0.5),(0.6*0.9),(0.9*0.8)\}$  
$\qquad =\max\{0.1,0.24,0.72\}=0.72$

Therefore the result obtained by max-product composition is

$\bar{R}_1 \circ \bar{R}_2=\begin{bmatrix}0.36&0.5\\0.03&0.03\\0.54&0.72\end{bmatrix}$

In the same manner as relations can be composed, the one-dimensional facts can be composed with the rule base to realize the reasoning operation. This can now be precisely re-formulated for the general case of a rule base.

If for the rule base

$R:X\times Y\longrightarrow[0,1]$

its membership function is described by Equations (6.16) or (6.17) and if there is a fact described by the fuzzy set

$A':X\longrightarrow[0,1]$

and its membership function $\mu_{A'}$, the result

$B':A'\circ R:Y\longrightarrow[0,1]$

of the fuzzy reasoning is represented by the membership function

$\mu_B(y)=\max_{x\in X}\{\min\{\mu_{A'}(x),\mu_R(x,y)\}\}$  (6.18)