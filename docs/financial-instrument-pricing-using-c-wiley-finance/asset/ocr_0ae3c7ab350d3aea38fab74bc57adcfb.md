+   e) How many steps in the binomial method are needed if we wish to get 6-digit accuracy? Apply the lattice methods of Chapters 11 and 12 to this problem. Anecdotal evidence suggests that between two and four million steps are needed using the binomial method.
+   
+   f) How many steps in the ADE method are needed if we wish to get 6-digit accuracy? Apply the methods of Chapters 20 to 23 to this problem. As indication, for NS = 2700 we get P = 6.28858, for NS = 5400 we get P = 6.299595 and for NS = 10800 we get P = 6.299596.

# 7. (Barrier Options)

We have introduced barrier options and their numerical approximation using BTCS (fully implicit scheme) and exponential fitting in Section 25.7 and we produced several tables of values for reference purposes. In this exercise we wish to price barrier options using the MOL.

Answer the following questions:

+   a) Compare the possible advantages of the MOL with the finite difference schemes in Chapters 20 and 21 with regard to ease of programming, supporting functionality (for example, the eight barrier types, their prices and sensitivities), continuous and discrete monitoring and robustness (for example, behaviour near a barrier close to expiry).
+   
+   b) Create a software framework using the MOL as a variation of the code in these chapters. Pay particular attention to modelling boundary conditions, rebates and so on.
+   
+   c) Write code to numerically compute the delta and gamma of barrier options. Display them using the Excel driver as discussed in Chapters 14 and 22 (in particular, Section 22.4).
+   
+   d) Based on the output from part c), compare values with plain options from a financial viewpoint (see Derman and Kani, 1996).

# 8. (Compound Options, Project)

The objective of this exercise is to price compound options using the binomial method. A *compound option* is an option on an option. Its payoff involves the value of another option executed either concurrently or in sequence. Thus, a compound option has two expiration dates and two strike prices in general. These options are used for currency and fixed-income markets and to hedge bids for business projects that may or may not be accepted (Mun, 2002). There are two steps in pricing a compound option:

+   ▪ Price the underlying option.
+   ▪ Price the compound option.

For example, the payoff of a *call on a call option* with exercise price K₁ for the underlying and K₂ for the compound option is given by:

$$F(S) = \max(S-K_1,0)$$
$$G(V_2) = \max(V_2-K_2,0).$$

A compound option gives the owner the right to buy or sell another option. The four basic types are call on call, call on put, put on put and put on call.

We describe compound option pricing using PDEs. The PDE for the underlying option with expiration T₁ is given by:

$$\frac{\partial V_1}{\partial t}+\frac{1}{2}\sigma^2S^2\frac{\partial^2V_1}{\partial S^2}+rS\frac{\partial V_1}{\partial S}-rV_1=0$$
$$V_1(S,T_1)=F(S).$$