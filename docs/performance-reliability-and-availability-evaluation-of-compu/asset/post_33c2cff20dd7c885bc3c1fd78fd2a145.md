
Exercise 18. Find the minimal cuts and paths of RBD of Exercise 17.

Exercise 19. Find the minimal cuts and paths of RBD of Exercise 15.

Exercise 20. Calculate the structural importance of the system represented by the RBD of the Figure 18.41.

Exercise 21. Obtain the reliability importance (Birnbaum importance) of the tiny cloud system shown in Exercise 15.

Exercise 22. Calculate (a) the reliability importance (Birnbaum importance) and (b) availability importance of the tiny cloud system shown in Exercise 15.

Exercise 23. Compute the reliability sensitivity with respect to the system parameters of the tiny cloud system shown in Exercise 15.

Exercise 24. Consider the system shown in Figure 18.43. Calculate the following importance measures for each component of the system: (a) IP, (b) CIP, (c) RAW, (d) RRC, (e) $I^{CS}$, and (f) $I^{CF}$. Compare them and comment.

# 19 Fault Tree

This chapter introduces the Fault Tree (FT) model. FT and RBD are the most widely used combinatorial models for reliability and availability evaluation. As mentioned in the previous chapter, combinatorial models suppose the system components are statistically independent and have a low power concerning state-space models but with high analytic tractability.

Fault Tree Analysis (FTA) was initially developed in 1962 at Bell Laboratories by H. A. Watson to evaluate the Minuteman I Intercontinental Ballistic Missile Launch Control System. Afterward, in 1962, Boeing and AVCO expanded the use of FTA to the entire Minuteman II [129]. The operation of a system can be considered from two distinct perspectives. We can specify the correct behavior, or we enumerate the system failures [449]. Differently from RBDs, FT is a failure-oriented model, and as in RBDs, it was initially proposed for calculating reliability. Nevertheless, FT has also been extensively applied to evaluate other dependability metrics.

It is interesting to note that specific evident points in success-oriented models concur with certain analogous points in failure-oriented models. Thus, for instance maximum success in RBDs can be thought of as the corresponding minimum failure in FTs. Although our first inclination may be to choose the optimistic view of orthhetically, the number of conditions in which a system can fail and the number of conditions a system can successfully operate are without unlimited, from a practical point of view, there are usually more ways to specify the system operation than the system failures. Thus, from a practical perspective, the set of events representing the successful system operation.

The Fault Tree is a graphical model that depicts logical relations between components' FT that result in a system failure.

# 19.1 COMPONENTS OF A FAULT TREE

In FT, the system may be represented by a logical function that is evaluated as true whenever at least one minimal cut is evaluated. The system state may also be characterized by a structure-function, which is the opposite of the RBDs. If the system has more than system failure, a logical function (or a structure-function) should be specified for representing each failure mode. In other words, one function should be defined for representing the combination of events that cause each system failure.

The most common FT elements are the TOP event, AND, OR, and self gates, and basic events. Many extensions have been proposed; some of them adopt XOR, Performance, Reliability, and Availability Evaluation of Computational Systems transfer, and priority gates (see Table 19.1). This chapter, however, does not cover these extensions.

# Table 19.1: Fault Tree - Components

| Description | Graphical Notation |
| --- | --- |
| TOP Event | ◯ |
| Basic events | △ |
| Repeated basic event. | ⬢ |
| AND gate | ⬢<br>▽<br>[AND]<br>—<br>◯ ◯ ◯ |
| OR gate | ⬢<br>▽<br>[OR]<br>◯ ◯ ◯ |
| KON gate | ⬢<br>▽<br>[KON]<br>◯ ◯ ◯ |
| KON gate (identical events) | ⬢<br>▽<br>[Round] |
| Comment rectangle | ▭ |

Assume a computational system S comprises two larger subsystems, a hardware subsystem (HS) and a software subsystem (SS). The hardware subsystem is composed of three subsystems: a motherboard component (MB), a power subsystem (PS), and a memory subsystem ($MS$). The power subsystem is composed of two hot-standby power sources ($PS_1$ and $PS_2$). The memory subsystem is composed of three memory banks ($M_1, M_2$, and $M_3$). The software subsystem has two components, the operating system ($OS$) and one application program ($AP$). The basic components are specified in the set $CS = \{PS_1, PS_2, M_1, M_2, M_3, MB, OS, AP\}$. This system is shown in Figure 19.1.

![](img/2d1450514bb14a0cdf0eb5048614afab_157_0.png)

Figure 19.1 Computational System.

As in Section 18.3, the state of each basic component $i$ may be represented by the logical variables $x_i$. The complement of $x_i$ is $\overline{x}_i$, which denotes the component $i$ failure. We specify the state of system basic components by logical variables denoted by components' abbreviation $PS_1, PS_2, M_1, M_2, M_3, MB, OS$, and $AP$. Therefore, $PS_1, PS_2, M_1, M_2, M_3, MB, OS$, and $AP$ represent each component failure.

The top of an FT is usually placed at the top of the diagram, whereas gates and basic event are introduced below. Figure 19.2 shows an FT that represents the system depicted in Figure 19.1. This FT has four gates and eight basic events. A system failure occurs if the power system, the memory subsystem, motherboard, or software subsystem fails. The power system fails if both power sources fail, whereas the memory subsystem fails if three memory banks fail. The software subsystem fails if the operating system or application programs fail. The top event, that is, the system failure, is represented by the logical function

$\Psi(\mathbf{B}) = (PS_1 \wedge PS_2) \vee (M_1 \wedge M_2 \wedge M_3) \vee MB \vee (OS)$
$\mathbf{B} = (PS_1, PS_2, M_1, M_2, M_3, OS, AP)$ (see Equation 20.2).

If the system has more than one functionality (operation), logical functions should be specified for each functionality (failure mode). Hence, failed system for a particular operation does not mean it is failed for another functionality.

# 142 Performance, Reliability, and Availability Evaluation of Computational Systems

![](img/2d1450514bb14a0cdf0eb5048614afab_158_0.png)

Figure 19.2 Fault Tree - Computational Systems. The system state may also be specified by structure function of its components. The structure function is evaluated to zero whenever at least a minimal number of components fails (see Definition 18.3). The structure function is specified in terms of structure variables. A structure variable $x$ is evaluated to zero when component $i$ failed (see Definition 18.2). Let us define the structure variables $x_{ps1}, x_{ps2}, x_{m1}, x_{m2}, x_{m3}, x_{mb}, x_{os}$, and $x_{ap}$ for representing the states of the system shown in Figure 19.1. The structure function can be obtained from the logical function, since

$\Psi(B) = (PS_1 \wedge PS_2) \vee (M_1 \wedge M_2 \wedge M_3) \vee MB \vee (OS)$
$\Psi(B) = (PS_1 \wedge PS_2) \vee (M_1 \wedge M_2 \wedge M_3) \vee MB \vee (OS)$
$\Psi(B) = (PS_1 \wedge PS_2) \wedge (M_1 \wedge M_2 \wedge M_3) \wedge MB \wedge (OS \wedge AP)$

Applying the transformation rules depicted in Table 18.3, we obtain

$\Phi(X) = (1 - x_{ps1}) \times (1 - x_{ps2}) \times (1 - (1 - x_{m1}) \times (1 - x_{m2})) \times (1 - x_{m3}) \times x_{mb} \times x_{os} \times x_{ap}$.

If the expected value of $x_i$ is the component $i$ reliability, $E(x_i) = R_i(t)$, the system reliability is $R_s(t) = E(\Phi(X))$; then

$R_s(t) = E((((1 - x_{ps1}) \times (1 - x_{ps2})) \times (1 - (1 - x_{m1}) \times (1 - x_{m2}) \times (1 - x_{m3}))) \times x_{mb} \times x_{os} \times x_{ap})$.

Therefore

$R_S(t) = (1 - (1 - E(x_{ps1}))) \times (1 - E(x_{ps2}))) \times (1 - E(x_{m1})) \times (1 - E(x_{m2}))\n\times(1 - E(x_{m3})) \times E(x_{mb}) \times E(x_{os}) \times E(x_{ap}).$.

$R(t) = (1 - (1 - R_{ps1}(t))) \times (1 - R_{ps2}(t)) \times (1 - R_{m1}(t)) \times (1 - R_{m2}(t))\n\times(1 - R_{m3}(t)) \times R_{mb}(t) \times R_{os}(t) \times R_{ap}(t).$.

**Example 19.1.1.** Assume the time to failure of each basic component is exponentially distributed with the respective rates $\lambda_{ps1} = \lambda_{ps2} = 6.67 \times 10^{-5} f/h, \lambda_{m1} = \lambda_{m2} = \lambda_{m3} = 3.33 \times 10^{-5} f/h, \lambda_{mb} = 2.5 \times 10^{-5} f/h, \lambda_{os} = 2.5 \times 10^{-4} f/h, and \lambda_{ap} = 5 \times 10^{-4} f/h.$.

The system reliability is

$R(t) = (1 - e^{-\lambda_{ps1}t}) \times (1 - e^{-\lambda_{ps2}t}) \times (1 - e^{-\lambda_{m1}t}) \times (1 - e^{-\lambda_{m2}t})\n\times(1 - e^{-\lambda_{m3}t}) \times e^{-\lambda_{mb}t} \times e^{-\lambda_{os}t} \times e^{-\lambda_{ap}t}.$.

$MTTF = \int_{0}^{\infty} R(t)dt = 1274.88 h$ and the reliability curve is shown in **Figure 19.3**.$.

![](img/2d1450514bb14a0cdf0eb5048614afab_159_0.png)

**Figure 19.3** $R(t) \times t.$.
