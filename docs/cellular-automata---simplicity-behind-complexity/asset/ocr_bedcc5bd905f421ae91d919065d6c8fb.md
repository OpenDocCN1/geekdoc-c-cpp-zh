$$\frac{\partial}{\partial t}p(x,y,t)=g_p(x,y,T)+\frac{1}{q_p}\nabla_J p(x,y,t)$$

$$\frac{\partial}{\partial t}r(x,y,t)=g_r(x,y,T)-\frac{1}{q_p}\nabla_J r(x,y,t)$$

where $[p(x,y,t);\ r(x,y,t)]$ represents the surface concentrations of both pseudo particles, inhabitants and recursions, $[g_p(x,y,T);\ g_r(x,y,T)]$ their speeds of growth and $[J_p(x,y,t);\ J_r(x,y,t)]$ the corresponding current densities, for which a *population equivalent charge* $q_p$ will be defined afterwards. Besides, the growth part of the transport model specified in the pair of equations (18) follows the form:

$$\delta p=\eta_p\rho_0-\gamma\,r/\rho_0$$

$$\delta r=\eta_r\rho_0-\beta\,r/\rho_0$$

where $\delta p=g_p\cdot\Delta t$ and $\delta r=g_r\cdot\Delta t$ represent the variations of concentrations of pseudo particles in a $\Delta t$ interval, $\eta_p$ and $\eta_r$ their free growth rates, $\gamma$ a factor of mutual control of population and $\beta=r_0/r_0$ an urban quality factor, with $\rho_0$ and $r_0$ the respective local stationary concentrations at statistical “temperature” $T_0$. Thus, the growth for each pseudo particle adopts the form of a balance between generation (production) and recombination (loss), as it could happen in the case of doped solid materials because of extrinsic excitation, a form that in addition can be linked to a prey-predator model typical of population dynamics in ecology (see for example: Bossel H., 1986; Pacala S. and Levin S., 1997). This requires the definition of population and resources growth rates, and of a recombination rate, that here is to be interpreted as a cross limitation to the free rates of growth.

As for the circulatory part of the transport model, this one follows the form:

$$\frac{1}{q_p}J_p(x,y,z,t)=-\mu_p\,p\nabla V+D_p\nabla p$$

$$\left(\frac{1}{q_p}\right)J_r(x,y,z,t)=-\mu_r\,r\nabla V-D_r\nabla r$$

Currents adopt in each case the form of a dynamic balance between a drift current, mobilized by the gradient of an *urban potential*, and a diffusion current, mobilized by the gradient of the corresponding concentration. Currents demand the definition of an appropriate urban potential (in which the population charge mentioned above takes part), and a spatial tensor of mobility and diffusion $[\mu_p,D_p;\ \mu_r,D_r]$.

This type of transport and growth model is naturally attainable by means of bidimensional cellular automata of mobile agents, characterized by a set of parameters that are a function of space and of the statistical temperature of the system. Hereby, nevertheless, the additional advantage lays in that the analogy with the solid state of matter allows a more conceptual bottom-up interpretation, diminishing therefore the necessities of model parameterization to an indispensable minimum.

# 3.3 Urban potential and the population equivalent charge

From the point of view of the individual contribution of an inhabitant, the urban potential represents a measurement of its energy reserve, as a result of the capacity of the individual to collect resources from the environment, as seen already for the biotautomaton. Appart from what is stated in ec. (2), it can also be defined by means of a bottom-up approach analogous to Thomas-Fermi model, used in solid state physics (Kittel C., 1995), taking