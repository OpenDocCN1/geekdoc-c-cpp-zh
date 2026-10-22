
Parameters of input variables are usually organized in the first stage, then the next important input parameters in the second stage, and so on. In this work, we consider the case where the fuzzy rule base consists of $M$ stages in the following forms:

Stage 1 :
IF $x_0$ is $A_{1,0}^1$ ∧ ⋯ ∧ $x_{L_1}$ is $A_{1,L_1}^1$
THEN $y_1$ is $B_1^1$
⋯
IF $x_0$ is $A_{n,0}^1$ ∧ ⋯ ∧ $x_{L_1}$ is $A_{n,L_1}^1$
THEN $y_1$ is $B_n^1$
⇒ (output to 2nd stage)

Stage 2 :
IF $y_1$ is $A_{1,1}^2$ ∧ ⋯ ∧ $x_{L_2}$ is $A_{1,L_2}^2$
THEN $y_2$ is $B_1^2$
⋯
IF $y_1$ is $A_{n,1}^2$ ∧ ⋯ ∧ $x_{L_2}$ is $A_{n,L_2}^2$
THEN $y_2$ is $B_n^2$
⇒ (output to 3rd stage)

Stage $m$ :
IF $y_{m-1}$ is $A_{1,m-1}^m$ ∧ ⋯ ∧ $x_{L_m}$ is $A_{1,L_m}^m$
THEN $y_m$ is $B_1^m$
⋯
IF $y_{m-1}$ is $A_{n,m-1}^m$ ∧ ⋯ ∧ $x_{L_m}$ is $A_{n,L_m}^m$
THEN $y_m$ is $B_n^m$
⇒ (to control input)

where ∧ is ‘and’ operator, $A_{j,k}^i$ and $B_j^i$ are linguistic terms characterized by fuzzy membership functions $\mu_{A_{j,k}^i}(x)$ and $\mu_{B_j^i}(y_i)$, respectively, ($i=1,2,\ldots,m$; $j=1,2,\ldots,n$; $k=0,1,\ldots,L_i$); $x_k$ and $y_i$ ($i=1,\ldots,m-1$) in the IF-parts are input and intermediate variables, respectively, and $y_m$ in the THEN-parts is the output variable.

## 5.2.1 Multistage fuzzy inference engine

The multistage fuzzy inference engine is decision-making logic, which employs fuzzy rules from the fuzzy rule bases, to determine a mapping from the fuzzy sets in the input universe of discourse $U_x$ to the fuzzy set in the output universe of discourse $U_y$. For the $i$-th inference stage, let $A_x^i$ be an arbitrary fuzzy set in $U_x$; then each rule $R_j^i$ in the $i$-th stage determines a fuzzy set $A_x^i \circ R_j^i$ based on the t-norm operator:

\[
\begin{aligned}
\mu_{A_x^i \circ R_j^i}(y)
&= \sup_{X \in U}\left[\mu_{A_x^i}(X) * \mu_{A_{1,j}^i}(x_1) * \cdots * \mu_{A_{L_i,j}^i}(x_{L_i}) \to \mu_{B_j^i}(y_i)\right] \\
&= \sup_{X \in U}\left[\mu_{A_x^i}(X) * \mu_{A_{1,j}^i}(x_1) * \cdots * \mu_{A_{L_i,j}^i}(x_{L_i}) * \mu_{B_j^i}(y_i)\right]
\end{aligned}
\tag{5.1}
\]

When facts are given, the fuzzy rules in the first stage are inferred, and then the consequences of the intermediate variables in the inference stage are formulated before they are passed on to the next stage as facts. This can easily be illustrated by an example with two inputs and one output at inference stage 1, and three fuzzy rules. The general scheme and reasoning structure of multistage inference are shown in Fig. 5.5 and Fig. 5.6, respectively.

![](img/ffb89ef8c668ade3e6e47a9ee7de70e5_193_0.png)

Figure 5.5 A general scheme of multistage fuzzy inference system

## 5.2.2 Multistage fuzzy inference procedure

In general, the fuzzy inference procedure consists of the following steps:

1. Read inputs and fuzzify inputs into input facts.
2. Perform match-degrees among inputs and those if-clauses of fuzzy rules that involve input variables.
3. Compute the firing strengths of the fired fuzzy rules.

![](img/ffb89ef8c668ade3e6e47a9ee7de70e5_194_0.png)

Figure 5.6 The architecture of multistage fuzzy logic inference

4. Calculate the conclusion by deriving the consequences of intermediate output variables of the $i$-th stage, where $i$ is not the final one, and normalize these derived consequences.
5. Pass the conclusions in the $i$-th stage onto the next stage as input facts. By a similar process, the conclusion may be defuzzified and then passed onto the next stage as a fact when the conclusion is too fuzzy in the reasoning. Repeat step 1 to step 5 until the multi-stage fuzzy rules in all inference stages are inferred.
6. Perform the conclusions of output variables of the final stage when all fuzzy rules in every stage have been inferred.
7. Calculate defuzzification to obtain a singleton to be the control input.

An algorithmic description of the above procedure is expressed as follows:

```
Algorithm multistage fuzzy logic inference(){
    // inputs: input variable (tracking errors)
    // output: obtained control input
    Do while (not halt){
        Input-fuzzy();
        // Fuzzification process for input data to
        // obtain input facts
        If-clause-evaluate();
        // input facts are broadcasted to all
        // if-clauses to compute match-degrees
        If-part-evaluate();
        // Match-degrees are taken as inputs
        // to evaluate firing strengths

        // intermediate variable derived as follows:
        for stage 2 to stage m {
            Then-part-evaluate();
            // deriving then-part fuzzy values and
            // normalizing them (sometimes defuzzifying them)
            // to obtain consequence (except final stage)
            If-clause-evaluate();
            // Either the fuzzy set conclusion or the
            // defuzzified singleton value are
            // broadcasted to all if-clause
            If-part-evaluate();
            // Match-degrees are taken as inputs
            // to evaluate firing strength
        } // end for
        Then-part-evaluate();
        // Deriving then-part fuzzy values and normalizing
        // then at the final stage to obtain consequence
        Defuzzy-output();
        // perform defuzzification to obtain control
        // input for the output variable
    } // end do while
} // end multistage fuzzy logic inference
```

## 5.3 Methodology of fuzzy rule generation

The fuzzy rule base is the heart of a fuzzy control system in the sense that all other design parameters are used to assist and interpret these fuzzy rules and make them usable to design a fuzzy controller for a specific control problem.

where $GU_m$ is the output scale factor of the $m$-th stage and
\[
f_m(e_m, u_{m-1}) = -\frac{|u_{m-1}| u_{m-1} + |e_m| e_m}{\Delta}.
\]
The rule-generated function of the $m$-th stage is obtained from $f_m(e_m, u_{m-1})$ in which $e_m$ and $u_{m-1}$ are replaced by their index $I_m$ and $I_{m-1}$ of the fuzzy subsets $A_{I_m}$ and $A_{I_{m-1}}$ in Eq. (5.5), respectively,

\[
f_m(I_m, I_{m-1}) = \operatorname{sat}\left(n, -\frac{|I_m| I_m + |I_{m-1}| I_{m-1}}{\Delta'}\right)
\tag{5.10}
\]

where $\Delta' = \sqrt{I_m^2 + I_{m-1}^2}$, and $\operatorname{sat}(n, x)$ stands for a saturation function:

\[
\operatorname{Sat}(n,x)=
\begin{cases}
n, & \text{if } x \ge n,\\
\operatorname{round}(x), & \text{if } -n < x < n,\\
-n, & \text{if } x \le -n
\end{cases}
\tag{5.11}
\]

where $n$ is the maximum index of fuzzy linguistic terms and $\operatorname{round}(x)$ can truncate $x$ into an integer.

From Eq. (5.8), the most negative gradient $-|\nabla I_j|$ implies that $u_{m-1}$ is maximum. Thus we take the positive gradient of $u_j$ for the $j$-th stage as

\[
|\nabla u_j| = \left[ \frac{|e_j(k)|}{\Delta_j} \quad \frac{|u_{j-1}(k)|}{\Delta_j} \right]
\tag{5.12}
\]

where $\Delta_j = u_j$. Using a similar method, the output of the $j$-th stage is chosen as

\[
y_j(k) = GU_j(|\nabla u_j|) \begin{bmatrix} e_j(k) \\ u_{j-1}(k) \end{bmatrix}
= GU_j\left(\frac{|e_j(k)| e_j(k)}{\Delta_j} + \frac{|u_{j-1}(k)| u_{j-1}(k)}{\Delta_j}\right)
= GU_j * f_j(e_j, u_{j-1})
\tag{5.13}
\]

The rule-generated function of the $j$-th stage is obtained from $f_j(e_j, u_{j-1})$ in which $e_j$ and $u_{j-1}$ are replaced by their index $I_j$ and $I_{j-1}$ of the fuzzy subsets $A_{I_j}$ and $A_{I_{j-1}}$, respectively,

\[
f_j(I_j, I_{j-1}) = \operatorname{sat}\left(n, \frac{|I_j| I_j + |I_{j-1}| I_{j-1}}{\Delta_j}\right)
\tag{5.14}
\]

For example, assume that the fuzzy set $F$ in which every fuzzy subset is associated with an integer is expressed as $F = \{NB_{-3}, NM_{-2}, NS_{-1}, ZO_0, PS_1, PM_2, PB_3\}$. One fuzzy rule in the $j$-th subsystem with two inputs and single output can be coded with the form of an IF-THEN clause: IF $y_{j-1}$ is $NB_{-3}$ and $e_j$ is $NB_{-3}$ THEN $y_j$ is $PB_3$, where the integer 3 of the fuzzy subset $PB_3$ is obtained from the Equation

\[
f(-3, -3) = \operatorname{sat}\left(3, \frac{-|-3|*(-3) - |-3|*(-3)}{\Delta'}\right) = 3
\]

(Eq. 5.14), where $\Delta' = \sqrt{(-3)^2 + (-3)^2}$.

The key advantage of using multi-stage structure of fuzzy logic is that the number of rules will increase only linearly (not exponentially) with the number of variables. But the latency time (i.e., inferring time) of the multi-stage fuzzy logic inference, the number of fuzzy set operations of input, output, and intermediate variable must be reduced as much as possible. This can be solved by pre-computing the fuzzy set operations on several multi-stage fuzzy rules to shorten the latency time. Thus, the number of the match-degree calculations for input variables may decrease as well as the numbers of the conclusion formulations and defuzzification operations for output variables may decrease. For the intermediate variables, the fuzzy set operations can be pre-computed at compiling time; besides, the numbers of intersection and union scalar operations can be reduced in order to speed up reasoning at execution time. Therefore, the latency time involved in multi-stage fuzzy logic inference can be effectively reduced.

## If-part evaluations of fuzzy rules at any stage

To describe the method, the notation of fuzzy values of variables is adopted in which the fuzzy values of the intermediate variable $y_{i-1}$ are $\{FuzzyValue_h\}$ of the intermediate variable $y_{i-1}$ in the $i$-th stage, which are denoted by $\{FV_h^i(y_{i-1})\}$, $1 \le i \le m$, $h \in \{1,\cdots,l_i\}$, and the linguistic terms of IF-part are expressed as

\[
A_{j,k}^i \in \{FV_h^i(y_{i-1})\},
\tag{5.15}
\]
\[
1 \le i \le m, \quad j \in \{1,\cdots,n_i\}, \quad 1 \le k \le m-1, \quad h \in \{1,\cdots,l_i\}
\]

where $n_i$ is the number of the $i$-th stage fuzzy rules, and $l_i$ is the number of fuzzy values of the intermediate variable $y_{i-1}$ in the $i$-th stage. When an input fact or an inferred one occurs, the match-degrees among $FV_h^i(y_{i-1})$s in the $i$-th stage are performed with the fact as follows:

\[
\alpha_h^i(y_{i-1}) = \max_{u^{i-1} \in U_{y_{i-1}}} \left( \mu_{FV_h^i(y_{i-1})}(u^{i-1}) \wedge \mu_{\tilde{A}_i}(u^{i-1}) \right)
\tag{5.16}
\]
\[
1 \le i \le m, \quad h \in \{1,\cdots,l_i\}
\]

where $\wedge$ means a T-norm operator. The T-norm operators commonly chosen for the intersection operations are the logical, algebraic, bounded, and drastic product operators, whereas the S-norm operators for the corresponding union operations are the logical, algebraic, bounded, and drastic sum operators.

When these non-zero match-degrees are evaluated, they are broadcasted to those if-clauses which involve the fuzzy value $FV_h^i(y_{i-1})$. So the firing strength of rule $R_j^i$ can also be derived from Eq. (5.17):

\[
\alpha_{jT}^i = \wedge \alpha_h^i(y_{i-1}), \quad 1 \le i \le m, \quad j \in \{1,\cdots,n_i\}, \quad h \in \{1,\cdots,l_i\}
\tag{5.17}
\]
