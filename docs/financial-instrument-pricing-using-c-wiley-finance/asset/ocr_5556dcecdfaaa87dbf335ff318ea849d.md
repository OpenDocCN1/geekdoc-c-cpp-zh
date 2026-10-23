In order to identify collaborations we ask the following questions for each responsibility of each class:

+   - Is the class capable of fulfilling a given responsibility by itself?
+   - If not, what does the class need?
+   - From which other classes can the class acquire what it needs?

Knowing what the inter-class relationships are will be useful in identifying collaborations. The major relationships are:

+   - **R1: Composition** (‘is part of’). These are also called *Whole–Part* and aggregation relationships (see POSA, 1996).
+   - **R2: Has knowledge of.** This relationship is a more loosely coupled version of composition. In general, class *X* has knowledge of class *Y* if *Y* can provide information to *X*.
+   - **R3: Depends on.** This is similar to relationship R2 but the classes forming the relationship do not necessarily have to know about each other. A third-party mediator may know about the dependency, for example.

Having described what coupling is we now define the corresponding metrics:

+   - **M10:** The number of other classes that a given class collaborates with.
+   - **M11:** The amount of collaboration with other classes.

The metrics M10 and M11 will take on another form when we discuss software development based on system decomposition and interface specifications in Chapter 9. At that stage object-oriented technology fades into the background somewhat.

# 7.6.4  Class and Member Function Inheritance

This group of metrics revolves around the quality when we use inheritance:

+   - **M12:** Class hierarchy nesting level. This refers to the depth of the inheritance tree.
+   - **M13:** Number of abstract classes.
+   - **M14:** Use of multiple inheritance.
+   - **M15:** Number of member functions overridden by a derived class.
+   - **M16:** Number of member functions inherited by a derived class.
+   - **M17:** Number of member functions added by a derived class.

In general (as we discussed in Section 7.5) inheritance is a mixed blessing and we tend to avoid using it too much for the reasons alluded to in that section. We also have a number of alternative designs to reduce the numerical values corresponding to the metrics M12 to M17. It is clear that the higher the numerical value, the more difficult it is to maintain the class hierarchy and the less likely that it retains its *semantic integrity*. Some ways to reduce the value are:

+   1. Use static polymorphism with CRTP instead of subtype/dynamic polymorphism.
+   2. We could pretend that we live in an inheritance-free world and use composition throughout. But this approach is probably not realistic.