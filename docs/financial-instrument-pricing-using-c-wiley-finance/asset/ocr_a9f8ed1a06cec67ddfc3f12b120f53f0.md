We introduce and describe the following software prototypes:

+   - P1: A *monolithic program* (‘ball of mud’) that prices one-factor plain call and put options using the explicit Euler method. This prototype functions as a requirements document and *feature list* (in the sense of the discussion in Section 9.3.2) that can be extended in later prototypes.
+   - P2: A solution based on policy-based design (PBD) and templates as discussed in Section 9.3.4.
+   - P3: This is a variation of solution P2 in which class hierarchies based on subtype/dynamic polymorphism are replaced by the *Curiously Recurring Template Pattern* (CRTP). CRTP is described in Chapter 21 (in particular, Section 21.7.2) where we apply it to PDE models.
+   - P4: A design based on the approach that we introduced in Section 6.8 that will be presented in Chapter 32. In this case we try to play down the role of classes and objects and focus more on system decomposition and the implementation of inter-component interface contracts using universal function wrappers (the class `std::function`).

There is no unique way to choose which prototypes to develop or in which order. However, there is a wrong way and a right way. In practice, customer and market requirements will determine how a software project evolves. We now discuss this topic.

# 31.1.1 Software Product and Process Management

From a software process viewpoint, the approach in this chapter is similar to that in the *Spiral Model* (Boehm, 1986). The spiral model is a risk-driven process for software projects. Based on the unique risk patterns of a given project, the spiral model guides a team to adopt elements of one or more process models, such as incremental, waterfall or evolutionary prototyping. The basic principles are (www.wikipedia.org):

+   a) Focus is on risk assessment and on minimising project risk by breaking a project into smaller segments and providing more ease of change during the development process, as well as providing the opportunity to evaluate risks and weigh consideration of project continuation throughout the life cycle.
+    b) Each cycle involves a progression through the same sequence of steps, for each part of the product and for each of its levels of elaboration, from an overall concept-of-operation document down to the coding of each individual program.
+    c) Each trip around the spiral traverses four basic quadrants: (1) determine objectives, alternatives, and constraints of the iteration, (2) evaluate alternatives; identify and resolve risks, (3) develop and verify deliverables from the iteration and (4) plan the next iteration. We begin each cycle with an identification of stakeholders and their “win conditions”, and we end each cycle with review and commitment.

We see Boehm’s *Spiral Model* as complementing the approach taken in Chapter 9. It is a *process driver* that helps deliver more functionality after the completion of each cycle. It is not the only model around and it may not be the best one in all cases. A discussion of the relative merits of the competing software development processes (such as *Agile* and *Waterfall*) is outside the scope of this chapter. See Exercise 1 where we discuss the spiral model from a project management viewpoint.