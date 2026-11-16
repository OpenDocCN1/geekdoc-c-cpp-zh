# Realistic Cloth Animation Using the Mass-Spring Model

Juan M. Cordero, Dep. de Lenguajes y Sistemas Informáticos, Universidad de Sevilla
cordero@lsi.us.es

Although cloth is a common object, the physical laws that govern its dynamics are complex. Continually, algorithms for cloth animation are improved by focusing on two main aspects: the efficiency of the models and the search for realistic results.

Since the mid-eighties, several cloth simulation models have been proposed based on geometric [Weil86], physical [Provot95, House00], and hybrid [Baraff98] properties. For the moment, only models based on physics provide realistic results. However, physical models are time-consuming processes due to the complexity of calculations and the difficulty of creating user-friendly methods for specifying material characteristics.

In recent years, the Kawabata Evaluation System (KES) [Kawabata75] has been used in cloth simulation models to empirically obtain parameters intrinsic to a particular type of cloth. However, KES is a costly technique, and in most cases, relatively few of the obtained results are used in the simulation models.

This gem details a new simulation method based on the mass-spring model that achieves high-quality results with a low computational cost. In the next section, we describe a computational model for cloth based on masses and springs. After that, we present the forces involved in cloth dynamics. We then outline the equations of the dynamic system and provide an approach to resolve them. Finally, we present our conclusions and identify directions for further research.

# A Discrete Representation of Cloth

A rectangular piece of cloth can be represented by a mesh of n x m mass particles linked by springs, as shown in Figure 4.3.1.