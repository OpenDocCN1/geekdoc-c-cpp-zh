Try to minimize the number of classes that depend on each other. The point is, if a class A is unaware of the existence of a class B, it is also unconcerned about any changes to B. (And this means that changes to B do not introduce bugs into A.) In software engineering terminology, you want to minimize the *coupling* between classes.

The *aggregation*, or “has–a” relationship, is easy to understand because it is concrete; for example, an Order object contains Item objects. Containment means that objects of class A contain objects of class B.

![](bbox=[0.128, 0.324, 0.181, 0.366])

> **NOTE:**
> 
> Some methodologists view the concept of aggregation with disdain and prefer to use a more general “association” relationship. From the point of view of modeling, that is understandable. But for programmers, the “has–a” relationship makes a lot of sense. I like to use aggregation for another reason as well: The standard notation for associations is less clear. See [Table 4.1].

The *inheritance*, or “is–a” relationship, expresses a relationship between a more special and a more general class. For example, a RushOrder class inherits from an Order class. The specialized RushOrder class has special methods for priority handling and a different method for computing shipping charges, but its other methods, such as adding items and billing, are inherited from the Order class. In general, if class D extends class C, class D inherits methods from class C but has more capabilities. (See the next chapter which discusses this important notion at some length.)

Many programmers use the UML (Unified Modeling Language) notation to draw *class diagrams* that describe the relationships between classes. You can see an example of such a diagram in [Figure 4.2]. You draw classes as rectangles, and relationships as arrows with various adornments. [Table 4.1] shows the most common UML arrow styles.