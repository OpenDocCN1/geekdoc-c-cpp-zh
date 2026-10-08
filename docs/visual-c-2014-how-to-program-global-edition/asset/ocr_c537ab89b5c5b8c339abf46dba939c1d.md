# 12.2 Polymorphism Examples

employees and for invoice amounts to be billed for purchased goods. As you'll see, interfaces enable polymorphic similarities to those enabled by inheritance.

# 12.2 Polymorphism Examples

Let's consider several additional examples of polymorphism.

# Quadrilateral Inheritance Hierarchy

If class Rectangle is derived from class Quadrilateral (a four-sided shape), then Rectangle is a more specific version of Quadrilateral. Any operation (e.g., calculating the perimeter or the area) that can be performed on a Quadrilateral also can be performed on a Rectangle. These operations can also be performed on Quadrilaterals, such as Squares, Parallelograms and Trapezoids. Polymorphism occurs when an agent invokes a method through a base-class variable—the correct derived version of the method is called, based on the type of the referenced object. You will see a sample code that illustrates this in Section 12.3.

# Video Game SpaceObject Inheritance Hierarchy

Another example, suppose we design a video game that manipulates objects of different types, including objects of Martian, Venus, Plutonian, SpaceShip and LaserBeam. Imagine that each class inherits from the common base class SpaceObject, which contains method Draw. Each derived class implements this method. A manager maintains a collection (a SpaceObject array) of objects to the various classes. To refresh the screen, the screen manager periodically sends each object the same message—Draw. However, each object responds in a unique way. For example, a Martian might draw itself with the appropriate number of antennae. A SpaceShip object might draw itself as a silver flying saucer. A LaserBeam might draw itself as a bright red beam across the screen. The same message (in this case, Draw) sent to a variety of objects has many results of from.

A screen manager uses polymorphism to facilitate adding classes to a system with minimal modifications to the system's code. To do so, we must build a Mercurian class that extends SpaceObject and provides its own Draw implementation. When objects appear in the SpaceObject collection, the screen manager invokes method Draw, exactly as it does for every other object in the class, regardless of its type, the new Mercurian objects simply "plug in" without any modification of the screen manager by the programmer. However, without modifying the system (other than build new classes and modify the code that creates objects), you can use polymorphism to include additional types that may not have been envisioned when the system was created.

![](bbox=[0.142, 0.833, 0.203, 0.893])

# Software Engineering Observation 12.1

> Polymorphism promotes extensibility: Software that invokes polymorphic behavior is independent of the messages which are sent. New object types that respond to existing method calls can be incorporated into a system without requiring modification of the polymorphic system. Only code that instantiates new objects must be modified to accommodate new types.