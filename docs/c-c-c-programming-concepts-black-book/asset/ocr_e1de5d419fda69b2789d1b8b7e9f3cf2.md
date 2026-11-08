# # Inheritance

The generalization hierarchy associates with it the idea of the process of inheritance. Two major types of inheritance are structural and behavioral. In the structural inheritance, a subclass inherits the attributes of its superclass. Suppose an employee class has name, address, and salary as its attributes. Then, a subclass, say engineer, can also be defined by using these attributes. In the behavioral inheritance, a subclass is said to inherit the methods of its superclass. Suppose the employee class has a method, calculatePay(). Then, a subclass, say manager, can also be characterized using this method.

A subclass also participates in the relationship sets in which its superclass participates. If a subclass has some subclasses specified on it, then it forms a hierarchy or a lattice. The class-subclass relationship is represented by a Directed Acyclic Graph (DAG). This is particularly useful when objects can be classified in more than one way, which are independent of each other.

If in a hierarchy, a given entity set is involved as a lower-level entity set in only one ISA relationship, then the entity set has **single inheritance**. Figure 13.9 shows the concept of single inheritance:

![](bbox=[0.27, 0.417, 0.71, 0.63])

**Figure 13.9: Showing the Concept of Single Inheritance**

If an entity set is a lower-level entity set in more than one ISA relationship, then the entity set has **multiple inheritance**, and the resulting structure is said to be a *lattice*. In a lattice or hierarchy, a subclass inherits the attributes not only of its direct superclass but also of all its predecessors. A subclass with more than one superclass is called a shared subclass. A shared subclass is a subclass in more than one distinct superclass–subclass relationship, where each relationship has a single superclass. Figure 13.10 shows the concept of multiple inheritance: