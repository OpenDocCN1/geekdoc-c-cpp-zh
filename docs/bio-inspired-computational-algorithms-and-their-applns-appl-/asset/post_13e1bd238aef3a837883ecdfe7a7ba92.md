
- Green, J. (2005). The Idea Behind Breeder Genetic Algorithm, *Department of Electrical Eng., University of Cape Town*.

- Folly, K. A. (2006). Design of Power System Stabilizer: A Comparison Between Genetic Algorithms and Population Based Incremental Learning, *2006 IEEE Power Engineering Society General Meeting*, ISSN: 1932-5517.

- Hemmati, R., Mojtaba, S., Boroujeni, S. & Abdollahi, M. (2010). Comparison of Robust and Intelligent Based Power System Stabilizers. *International Journal of the Physical Sciences*, Vol. 5, No. 17, pp. 2564-2573.

- Holland, J. H. (1975). *Adaptation in Natural and Artificial Systems*, University of Michigan Press, Ann Arbor.

- Hongesombut, K., Dechanupaprittha, S., Mitani, Y. & Ngamroo, I. (2005). Robust Power System Stabilizer Tuning Based on Multiobjective Design Using Hierarchical & Parallel Micro Genetic Algorithm. *Proc. of the 15th Power Syst. Comp. Conf.*, Liege.

- Ibraham & Ismail, Z. (2009). A Breeder Genetic Algorithm for Vehicle Routing Problem with Stochastic Demands. *Journal of Applied Research*, Vol. 5, No. 11, pp. 1998-2005.

- Kundur, P. (1994). *Power System Stability and Control*, McGraw Hill, 1994.

- Michalewicz, Z. (1996). *Genetic Algorithms + Data Structures = Evolution Programs*. 3rd Ed. Springer-Verlag.

- Mitchell, M. (1996). *An Introduction to Genetic Algorithms*, The MIT Press.

- Muhlenbein, H. (1994). The Breeder Genetic Algorithm—A Provable Optimal Search Algorithm and its Application, Available from http://www.ieee.org.

- Shetekela, S. & Folly, K. A. (2010). Breeder Genetic Algorithm for Power System Stabilizer Design. *2010 IEEE Congress on Evolutionary Computation (CEC)*, Barcelona, Spain.

- Shetekela (2010). *Design of Power System Stabilizer Using Evolutionary Algorithms*, MSc. Thesis, Department of Electrical Eng., University of Cape Town.

- Shaghoolian, G. & Faiz, J. (2010). The Effect of Power System Stabilizer on Small Signal Stability in Single Machine Infinite-Bus. *International Journal of Electrical and Power Engineering*, Vol. 14, No. 2, pp. 45-53.

- Sundareswara, K. & Begum, S. R. (2004). Genetic Tuning of a Power System Stabilizer. *Euro. Trans. Electr.*, Vol. 14, pp. 151-160.

- Tiako, R. & Folly, K. A. (2009). Investigation of Power System Stabilizer Parameters Optimisation using multi-power flow conditions. *Australian Journal of Electrical & Electronics Engineering*, Vol. 5, No. 3, pp. 237-244.

- Yoshimura, K. & Uchida, N. (2000). Optimization of P + ω Parameters for Stability and Robustness Enhancement in a Multimachine Power System. *Electrical Engineering in Japan*, Vol. 131, No. 1, pp. 19-31 (Translated from Denki Gakkai Ronbunshi, Vol. 11, Nov. 1998, pp. 1312-1320).

- Wang, Z., Chung, C. Y., & Wong, C. T. (2008). Robust Power System Stabilizer Design under Multi-Operating Conditions Using Differential Evolution. *IET Generation, Transmission & Distribution*, Vol. 2, No. 5, pp. 690-700.

## On the Application of Optimal PWM of Induction Motor in Synchronous Machines at High Power Ratings

Arash Sayyah<sup>1</sup> and Alireza Rezazadeh<sup>2</sup>  
<sup>1</sup>ECE Department, Boston University, Boston, MA  
<sup>2</sup>ECE Department, Shahid Beheshti University, Tehran  
<sup>1</sup>USA  
<sup>2</sup>Iran

### 1. Introduction

Distinctive features of synchronous machines like constant operation-speed, producing substantial savings by supplying reactive power to counteract lagging power factor caused by inductive loads, low inrush currents, and capabilities of designing the torque characteristics to meet the requirements of the driven load, have made them optimal options for a multitude of industries. Economical utilization of these machines and also increasing their efficiencies are issues that should receive significant attention.

At high power rating operations, where high switching efficiency in the drive circuits is of utmost importance, optimal pulsewidth modulation (PWM) is the logical feeding scheme (Holtz, 1992). Application of optimal PWM decreases overheating in machine and therefore results in diminution of torque pulsation. Overheating, resulted from internal losses, is a major factor in rating a machine. Moreover, setting up an appropriate cooling method is a particularly serious issue, increasing in intricacy with machine size. Among various approaches for achieving optimal PWM, harmonic elimination method is predominant (Mohan et al., 1995), (Enjeti et al., 1990), (Sun et al., 1996), (Chiasson et al., 2004), (Czarkowski et al., 2002), (Sayyah et al., 2006c). Since copper losses are fundamentally determined by current harmonics, defining a performance index related to undesirable effects of the harmonics is of the essence in lieu of focusing on specific harmonics (Bose, 2002). Herein, the total harmonic current distortion (THCD) is the objective function for minimization of machine losses.

Possessing asymmetrical structure in direct (d) and quadrature (q) axes makes a great difference in modeling of synchronous machines relative to induction ones. Particularly, it will be shown that the THCD in high-power synchronous machines is dependent upon some internal parameters of the machine; particularly $l_d$ and $l_q$, the inductances of d and q axes, respectively. Based on gathered input and output data at a specific operating point, these parameters are determined using online identification methods (Ljung & Söderstrom, 1983). In light of the identified parameters, the problem is reframed as an optimization task, and the optimal pulse patterns are sought through genetic algorithm (GA). Indeed, the complexity and nonlinearity of the proposed objective function increases the probability of trapping the

in which $\theta$ is the rotor angle. Neglecting the ohmic terms in (14), we have:

$$
\mathbf{u}_{\alpha\beta}
= \frac{d}{d\tau}\left(L_S(\theta)i_{\alpha\beta}
+ l_{md}\begin{pmatrix}\cos\theta\\ \sin\theta\end{pmatrix}i_F\right).
\tag{15}
$$

in which:

$$
L_S(\theta)=\frac{l_d+l_q}{2}I_2
+\frac{l_d-l_q}{2}\begin{pmatrix}\cos2\theta & \sin2\theta\\ \sin2\theta & -\cos2\theta\end{pmatrix}.
\tag{16}
$$

$I_2$ is the $2\times2$ identity matrix. Hence:

$$
\begin{aligned}
i_{\alpha\beta}
&=L_S^{-1}(\theta)\cdot\left(\int u_{\alpha\beta}\,d\tau
- l_{md}\begin{pmatrix}\cos\theta\\ \sin\theta\end{pmatrix}i_F\right)\\
&=\begin{pmatrix}
\frac{l_d+l_q}{2l_d l_q} - \frac{l_d-l_q}{2l_d l_q}\cos2\theta &
-\frac{l_d-l_q}{2l_d l_q}\sin2\theta\\
-\frac{l_d-l_q}{2l_d l_q}\sin2\theta &
\frac{l_d+l_q}{2l_d l_q} + \frac{l_d-l_q}{2l_d l_q}\cos2\theta
\end{pmatrix}
\cdot\left\{\int u_{\alpha\beta}\,d\tau
- l_{md}\begin{pmatrix}\cos\theta\\ \sin\theta\end{pmatrix}i_F\right\}\\
&=\left(\frac{l_d+l_q}{2l_d l_q}I_2
- \frac{l_d-l_q}{2l_d l_q}\begin{pmatrix}\cos2\theta & \sin2\theta\\ \sin2\theta & -\cos2\theta\end{pmatrix}\right)
\cdot\left(\int u_{\alpha\beta}\,d\tau
- l_{md}\begin{pmatrix}\cos\theta\\ \sin\theta\end{pmatrix}i_F\right).
\end{aligned}
\tag{17}
$$

With further simplification, we have $i_{\alpha\beta}$ as:

$$
i_{\alpha\beta}
= \frac{l_d+l_q}{2l_d l_q}\int u_{\alpha\beta}\,d\tau
+ l_1 - \frac{l_d-l_q}{2l_d l_q}l_2.
\tag{18}
$$

in which:

$$
l_1
= -l_{md}\frac{l_d+l_q}{2l_d l_q}\begin{pmatrix}\cos\theta\\ \sin\theta\end{pmatrix}i_F
+ l_{md}\frac{l_d-l_q}{2l_d l_q}
\begin{pmatrix}\cos2\theta & \sin2\theta\\ \sin2\theta & -\cos2\theta\end{pmatrix}
\cdot\begin{pmatrix}\cos\theta\\ \sin\theta\end{pmatrix}i_F.
\tag{19}
$$

and

$$
l_2
= \begin{pmatrix}\cos2\theta & \sin2\theta\\ \sin2\theta & -\cos2\theta\end{pmatrix}
\cdot\int u_{\alpha\beta}\,d\tau.
\tag{20}
$$

Using the trigonometric identities, $\cos(\theta_1 - \theta_2) = \cos\theta_1\cos\theta_2 + \sin\theta_1\sin\theta_2$ and $\sin(\theta_1 - \theta_2) = \sin\theta_1\cos\theta_2 - \cos\theta_1\sin\theta_2$, the term $l_1$ in Equation 18 can be simplified as:

$$
\begin{aligned}
l_1
&= -l_{md}\frac{l_d+l_q}{2l_d l_q}\begin{pmatrix}\cos\theta\\ \sin\theta\end{pmatrix}i_F
+ l_{md}\frac{l_d-l_q}{2l_d l_q}
\begin{pmatrix}\cos2\theta\cos\theta+\sin2\theta\sin\theta\\
\sin2\theta\cos\theta-\cos2\theta\sin\theta\end{pmatrix}i_F\\
&= -l_{md}\frac{l_d+l_q}{2l_d l_q}\begin{pmatrix}\cos\theta\\ \sin\theta\end{pmatrix}i_F
+ l_{md}\frac{l_d-l_q}{2l_d l_q}\begin{pmatrix}\cos\theta\\ \sin\theta\end{pmatrix}i_F\\
&= -\frac{l_{md}}{l_d}\begin{pmatrix}\cos\theta\\ \sin\theta\end{pmatrix}i_F.
\end{aligned}
\tag{21}
$$
