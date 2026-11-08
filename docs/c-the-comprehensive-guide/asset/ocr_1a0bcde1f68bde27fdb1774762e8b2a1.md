In this book, I primarily want to teach you the technical aspects and will only briefly touch on the conceptual aspects. However, you should be familiar with them in principle so that you are not at a loss during planning meetings.

# 15.1 Relationships

Relationships between objects play a central role in OOP as they significantly influence the structure and functionality of software and enable the modeling and organization of complex systems. In this context, the has-a and is-a relationships are of particular importance, as they define how objects are connected and how they relate to each other hierarchically.

# 15.1.1 Has-a Composition

When you learned about using `struct` and `class` in Chapter 12, I initially bundled data fields into *aggregates*.

```
```cpp
class Car {
    Windscreen windscreen_;
    std::vector<Wheel> wheels_;
    // ...
};
```
```

This Car *has-a* windscreen_ as well as wheels_—each of the corresponding type. In this case, a has-a relationship, Car is even composed of these objects or consists of these objects. This is a *composition*. That means the object usually *owns* its components—which in C++ means that it is responsible for their construction and destruction. The lifetime of the components is limited by the lifetime of the object.

![](bbox=[0.081, 0.634, 0.857, 0.671])

Figure 15.1 Has-a relationships: composition (left) and aggregation (right) in UML notation.

# 15.1.2 Has-a Aggregation

The situation is different when you say the car has-a car port or it has-a holder. This is an *aggregation*:

```
```cpp
class Car {
    CarPort& carPort_;
    Person& holder_;
    // ...
};
```
```