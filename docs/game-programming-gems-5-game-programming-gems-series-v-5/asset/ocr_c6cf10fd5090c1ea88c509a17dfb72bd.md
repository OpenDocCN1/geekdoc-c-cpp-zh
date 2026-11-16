# Component Based Object Management

Bjarne Rene, Circle Studio ltd
bjarne.rene@circle-studio.com

Traditional object management models often rely on inheritance hierarchies to share functionality between different types of objects. As games grow ever more complex, this approach leads to a design that is hard to change and where functionality is forced up the inheritance hierarchy if it is needed in several branches.

A good solution to this is to build objects from components, where each component is responsible for the data and behavior of one specific task. An object-management model based on this concept provides greater flexibility to create new objects and to modify existing behavior.

The first part of this gem outlines the differences between a traditional object-management system and a component-based system, and the main benefits gained from using the latter. The second part of the gem focuses on creating a component-based system from scratch. We conclude with a strong foundation for production-ready implementation.

# Out with the Old, In with the New

In a traditional object-management system, objects derive from the same abstract base class. For the purpose of this discussion, we consider such a system where all classes derive from the class cObject. The next step is to decide which classes derive from cObject. More often than not, the classes that derive directly from cObject are also abstract and represent a split in the tree between classes that have some functionality and classes that do not. Typical examples of such splits would be renderable/nonrenderable and animating/non-animating. Figure 1.3.1 shows a simple inheritance tree.

At first glance, this looks quite good, and the seduction of such a system is that it often does look very good on paper, at least for a little while. One thing we know about making games is that requirements change as development progresses. This model is not one that accommodates change to a satisfactory degree. Let us look at a few examples to illustrate.