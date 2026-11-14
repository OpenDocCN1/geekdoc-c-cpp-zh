![](bbox=[0.13, 0.07, 0.91, 0.5])

# Figure 9.37 Data and Control Flow Diagram for the Counter System

# 9.18 FUNCTIONAL MODEL VERSUS ARCHITECTURAL MODEL

With the architectural model formulated, in retrospect, a good question that one might ask at this stage is, “Why is it necessary to design a functional model and an architectural model?” Well, let’s see. We start by looking at any system – hardware, software, a mix, it doesn’t matter. It quickly becomes evident that the internal organization of a system is based on a collection of components and interconnections between them. An appropriate model has to include elements both at *functional level* and at the *architectural level* to be able to represent, design, and evaluate hardware/software systems. Such a distinction is an essential building block of the Co-Design methodology.

# 9.18.1 The Functional Model

The functional model describes a system through a *set of interacting functional elements*. The design proceeds at a high level without an initial bias toward any specific implementation. We have the freedom to explore, to be creative, to make hardware–software trade-offs. The behavior of a functional element is best described with a hierarchical and graphical model. The functional modules will interact using one of the following three types of relations:

+   • The *shared variable* relation, which defines a data exchange without temporal dependencies.