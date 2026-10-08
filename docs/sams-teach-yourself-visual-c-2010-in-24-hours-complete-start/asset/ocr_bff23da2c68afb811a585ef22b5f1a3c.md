object-oriented programming enables a new class to be created (called a child or **derived class**) that inherits the characteristics and behaviors from its parents (called base classes).

Inheritance enables you to reduce the apparent complexity of a problem into man-ageable parts. These parts form conceptual layers that provide increasing amounts of specialization or generalization, depending on your point of view, describing in a natural way the hierarchical nature of certain problems expressed using an "is-a" relationship.

# Watch Out!

# Multiple Inheritance

The general idea of inheritance is simple. However, many object-oriented program-ming languages enable derived classes to inherit from multiple parents, called multiple inheritance.
Multiple inheritance does not change the requirement that the classes have an "is-a" relationship, and can be a powerful mechanism, but that power can also result in considerable complexity in the implementation. It can also cause ambigiu-ity when trying to understand the derivation chain of a class because a class with two parents enables two different inheritance paths to a particular base class.
In order to remove the possible ambiguity and because the number of scenarios where multiple inheritance is the only appropriate solution is rather small, C# only allows single inheritance.

Typically, specialization is when the new class has additional data or behavior that is not part of the inherited (base) class. Specialization can also occur when the base class specifies that only an action or behavior exists but does not implement that behavior. It is then the responsibility of the derived classes to provide the implementation.

By creating a new type derived from an existing type, you inherit characteristics and behaviors from the parent type. Inheritance also enables derived classes to make sev-eral changes from their base class. The derived class can do the following:

+   - Add new private data.
- Add new behavior.
- Redefine existing behavior.

Again, taking the car example from last hour, Figure 4.1 shows a possible inheritance chain for a car. A car is-a four-wheel vehicle, which in turn is-a vehicle. The vehicle is the base, or root, class and provides behavior and data common for all vehicles. As