![](bbox=[0.094, 0.095, 0.493, 0.261])

Fig. 4. The $i_R-v_R$ curve for current-controlled resistor $R$ of Example 4. Here $i_R$ is a global coordinate for the curve. The resistor voltage $v_R$ does not qualify as a global coordinate. Nor does it qualify as a local coordinate at $Q_1$ and $Q_2$.

Hence, $Q_1$ and $Q_2$ are impasse points and we conclude that Fig. 4(a) represents a nonphysical circuit. To remodel this circuit, we need only insert a small series linear inductance representing the line inductance. It is easy to see that the resulting second-order circuit has a state equation defined globally in $\mathbb{R}^2$ [3].

To uncover the source of the difficulty in Fig. 4(b), note that since $q_C=v_C=v_R$, neither $q_C$ nor $v_C$ qualifies as a global coordinate, or as a local coordinate at $Q_1$ and $Q_2$.

The above “impasse point” phenomenon is truly unexpected even by mathematicians, and has never been reported in the mathematical literature.

Yet, by invoking a “jump postulate”, which Chua had justified by showing that the subsequent predictions agree with experimental observations [4], Chua had introduced a powerful and numerically much more efficient method for obtaining the correct result. Moreover, by applying his “dynamic route” technique, Chua was able to demonstrate, and explain the mechanism responsible for relaxation oscillations [11, 14]. This mechanism is illustrated in Example 1, page 1023 of [11], which we reproduce as Example 5 below:

is that starting in a small neighbourhood of $Q_2$ any computer simulation would get us to $Q_2$ in *finite time* $T$, after which the computer will be unable to continue the integration routine since the solution ceases to exist. Since all physical networks must have solution for all times $t\ge t_0$, any network which exhibits such impasse points is nonphysical and should be *remodeled*.

**Example 4.** Let $C$ in Fig. 4(a) be a 1-F linear capacitor and let $R$ be a *current-controlled resistor* described by

$$v_R=\hat v_R(i_R)\mathrel{\triangleq}\frac{1}{3}i_R^3-3i_R^2+8i_R,\qquad i_R\in\mathbb{R} \tag{23}$$

as shown in Fig. 4(b). Since $\hat v(i_R)$ is not bijective, $h(v_R)$ in (3) is multivalued over the interval $5\frac{1}{3}<v_R<6\frac{2}{3}$. Since both (3) and (6) are expressed in terms of $h(\cdot)$, *neither state equation exists globally* in this case. Note that this situation differs from those of Examples 2 and 3 where at least one state equation exists everywhere except for some isolated points.

To give a physical interpretation of this situation, observe that $\dot v_R=\dot v_C=i_C=-i_R$, implies $\dot v_R>0$ whenever $i_R<0$, and $\dot v_R<0$ whenever $i_R>0$. This gives rise to the dynamic route shown in Fig. 4(b). Again, we reach an impasse situation when the solution reaches $Q_2$ in some “finite” forward time $T<\infty$, or $Q_1$ in some “finite” backward time $T>-\infty$. (Note that $Q_1$ and $Q_2$ are not equilibrium points of either state equation (3) or (6), even if they are defined at $Q_1$ and $Q_2$.)

**Example 5.** Consider the $RL$ circuit shown in Fig. 5(a), where the resistor is described by a non-monotonic voltage controlled $v_R-i_R$ curve in Fig. 6(b). Since $di_R(t)/dt=-v_R$, it follows that $di_R(t)/dt<0$ whenever $v_R(t)>0$, and $di_R(t)/dt>0$ whenever $v_R(t)<0$. The dynamic route [3] showing this behavior is indicated by arrowheads in Fig. 5(b). Note that for any initial current $i_R$ other than at the origin, the solution reaches either $Q_1$ or $Q_2$ in finite time, beyond which the solution cannot be continued. Such points are called Impasse Points in [11]. The occurrence of impasse points in a network $N$ always gives rise to a nonphysical situation which requires that $N$ should be remodeled [11]. In this example, the simplest element (i.e., the lowest order element) that must be introduced to break the impasse is a linear capacitor, as shown in Fig. 5(c). The capacitance $C$ is usually a small number (say a few *picofarads*) chosen to simulate the “stray capacitance” between the wires. The state equation for the remodeled circuit in Fig. 5(c) is well defined (provided $C\ne0$)