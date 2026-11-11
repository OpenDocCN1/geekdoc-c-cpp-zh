# ■ **Inheritance**

Inheritance is a mechanism that allows a class to inherit properties and functionalities from another class. If the X class inherits properties from the Y class, then you can say that X has been inherited from Y. In this scenario, Y is called superclass or base class of X, and X is called a subclass or derived class of Y, as shown in Figure 1:

![](bbox=[0.421, 0.255, 0.599, 0.563])

▲ **Figure 1: Displaying Inheritance between X and Y Classes**

The objects of the X class have access to attributes and methods of the Y class. Objects of the subclass, X, can be used where objects of the corresponding superclass Y are required. This is because the objects of the subclass X share the same behavior as the objects of the superclass Y. Superclasses are also called parent classes and subclasses may also be called child classes or just derived classes.

Inheritance enables you to reuse the code of classes multiple times. This means that you can add additional features to an existing class without modifying it by deriving a new class from an existing class. In addition, you can define a subclass with some unique features that are different from the features already defined in the corresponding superclass. In addition to its own features, the new class contains the features of the parent class.