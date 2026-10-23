Consider issues such as shared/non-shared state, event-driven programming, maintainability and whether data is pushed or pulled.

d) Discuss the feasibility of implementing the SUD using variadic template parameters.

# 5. (Which Category Does an Application Belong to?)

In this book we discuss a number of applications in computational finance. In this exercise we wish to gain deep insights into understanding problems even before we write a single line of code. Consider the following applications:

+   - A1: Using the binomial method to price one-factor options.
+   - A2: Creating an interpolation library.
+   - A3: Affine pricing models for interest-rate derivatives.
+   - A4: Optimisation algorithms.
+   - A5: Parameter estimation algorithms.
+   - A6: One-factor and two-factor Monte Carlo option pricers.
+   - A7: Computing the mean error of a finite difference approximation of an SDE (see Kloeden, Platen and Schurz, 1997, p. 118).
+   - A8: Option pricing using PDE models.
+   - A9: Postprocessing routines to test the accuracy of a numerical scheme by comparison with a method that produces reference and exact values.
+   - A10: Creating data and modules to be used by other systems.
+   - A11: Configuring a complete application.

Answer the following questions:

a) Determine the category (or categories) that these applications are instances of. In general, the most important categories are MAN, RAT and MIS.

b) Create a basic system context diagram for these applications by identifying the systems and their responsibilities (use Figure 9.4 as reference model).

c) Identify the similarities and differences between the system context diagrams in the case of PDE, binomial and Monte Carlo option pricers.

d) Can you identify reusable artefacts such as code, libraries, data types and containers that can be used in multiple applications, for example the applications in part c)?

# 6. (Brainstorming, Starting a Software Project)

The next three exercises are meant to stimulate discussion on scoping and designing a software system and then packaging the code so that it can be used by clients. The intent will hopefully become even more clear as we progress through the book as many of the applications and examples adopt the same strategies. We are assuming in all cases that the five steps summarised in Section 9.8 will be adhered to for the purposes of the three exercises. The answers in all cases will tell us how to use and/or customise these steps to fulfil the given requirements.

The goal in this exercise is to scope the project and remove major ambiguities and risks before jumping into implementation details.

Answer the following questions by stating how to use the bespoke steps for the following requirements:

a) How to scope a project whose requirements are new to you (no precedence).

b) Create a proof-of-concept program to demonstrate to clients. You have a week in which to write the prototype.

c) Project estimation: estimate the numbers of hours to design the modules in the system context diagram.

d) Prioritising the modules: which ones to design now and which ones to design later?