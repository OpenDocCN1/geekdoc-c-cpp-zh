domain

$$H_n(s_1,\ldots,s_n)=\int_{-\infty}^{\infty}\cdots\int_{-\infty}^{\infty}h_n(\tau_1,\ldots,\tau_n)e^{-(s_1\tau_1+\cdots+s_n\tau_n)}d\tau_1\ldots d\tau_n.$$

In order to determine the Volterra kernels, we use the harmonic probing method [1]. This method is based on the application of a n-tone input signal $\sum_{k=1}^{n}e^{s_kt}$ in order to determine the Volterra-kernel of order $n$, e.g. to carry out the procedure for the first order needs an input of $x(t)=e^{st}$. The response can be directly calculated according to (12) as

$$y(t)=\sum_{k=1}^{\infty}H_k(s,\ldots,s)e^{kst}.$$

Using (14) and extracting an equation only for terms with the factor $e^{st}$, provides the first order kernel $H_1(s)$. The same procedure can be executed for higher order kernels and is explained in detail in [1].

# 4.2.  Theory of single memristor circuits

In this section we will apply the Volterra series approach to the general case of a SMC. Without loss of generality, we consider the linear part of the circuit being represented by its impedance matrix $\mathbf{Z}$. If the impedance matrix doesn’t exist for the circuit, one can use the admittance matrix and carry out a similar analysis. Also, without loss of generality, we define a current source providing the input signal $i_1$. The output signal then is the current $i_2$ flowing through the memristor. Knowing $i_2$, other circuit variables can be calculated by means of classical circuit theory. In order to describe a wider class of memristors, we use a polynomial model for the memristance

$$M(Q)=\sum_{k=1}^{\infty}m_kQ^k.$$

This approach holds for a charge controlled memristor, but it could be replaced as well by a flux dependent equation. The first term with $k=0$ was neglected in the sum (15) in order to separate the linear part from the nonlinear part of the circuit. However, if the memristor had a non-vanishing resistance at $Q=0$, it can be taken into account as a linear resistive one-port in the linear part of the circuit. In this case, we could redefine the function $M(Q)$ as a function $\widetilde{M}(Q)$ which already includes this substitution, i.e. we do not need to take care of this in the further analysis. Generally, the state variable Q does not denote the charge but is rather related to the charge and a constant summand, i.e. the time derivatives of both quantities are equal. Equation (15) represents also the HP-type memristor which just includes the first order. Please note that this approach also can include saturation effects. The linear system with its impedance operator fulfills the following dynamic equations

$$u_1=Z_{11}i_1+Z_{12}i_2$$
$$u_2=Z_{21}i_1+Z_{22}i_2,$$

where $Z_{ij}$ are the impedance matrix elements. Considering only the second row and replacing $U_2$ by the product of the current and the memristance, gives

$$Z_{21}i_1+Z_{22}i_2=u_2=-i_2\sum_{k=1}^{\infty}m_k\left(\int i_2dt'\right)^k.$$

So far, we have obtained a representation of the system which includes only the input current $i_1$ and the output current $i_2$. We now have to derive the Volterra kernels of different orders by applying the previously described methods. For the further calculation it is convenient to separate the different Volterra orders first. This is done by introducing a factor $c$ to the input $i_1$. As it is obvious from (12), the n-th order output $i_{2n}$ will be multiplied by a factor $c^n$. Equation (18) will hence become

$$Z_{21}ci_1+Z_{22}\sum_n c^ni_{2n}=-\sum_n c^ni_{2n}\sum_{k=1}^{\infty}m_k\left(\int\sum_n c^ni_{2n}dt'\right)^k.$$

This equation leads to a separation of the Volterra orders by simply sorting orders of $c$. The next step is to draw equations for each Volterra order out of (18) and afterwards to determine the Volterra kernels by means of an auxiliary n-tone input signal. The first order is represented by factors of the $c^1$ terms

$$Z_{21}i_1+Z_{22}i_{21}=0.$$

If the input is $i_1=1$, i.e. an amplitude “1” for the single tone signal $e^{j\omega_1t}$, for the output we get $i_{21}=H_1(\omega_1)$. Inserting these expressions into (19)