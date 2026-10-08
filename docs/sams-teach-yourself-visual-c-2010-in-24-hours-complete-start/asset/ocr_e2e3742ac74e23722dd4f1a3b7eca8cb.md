we go down the hierarchy, we find the four-wheel and two-wheel vehicle base classes, which are specializations of vehicle that add additional behavior and data. Finally, we find the car, truck, and motorcycle classes, which are derived classes that might also add additional behavior and data.

![](bbox=[0.25, 0.21, 0.85, 0.4])

In object-oriented programming, **polymorphism** is the capability of one type to be used like another type. Typically, there are two ways this is achieved:

+   - One type inherits (or derives) from another type, enabling it access to the same actions and public data as its parent.
- Both types implement a compatible public interface, enabling the same actions and public data but possibly different implementations.

Looking at the class diagram in Figure 4.1, it should be clear that although a car and a truck are clearly not the same type, either of those could be substituted for a four-wheel vehicle because they both inherit from that class. Likewise, although a motorcycle could not be substituted for a four-wheel vehicle, it could, along with a car or a truck, be substituted for a vehicle.

As you can see, polymorphism relies heavily on the ideas presented in encapsulation, abstraction, and inheritance. Without these aspects, it would be virtually impossible for one class to be substituted for another.

> **Polymorphism**
Polymorphism is one of those words that might sound like it is complicated, but it really isn’t. Polymorphism is a natural and common occurrence. The word is the combination of the Greek words poly (meaning many) and morphe (meaning shape or form), literally meaning many shapes or forms.

By the **Way**