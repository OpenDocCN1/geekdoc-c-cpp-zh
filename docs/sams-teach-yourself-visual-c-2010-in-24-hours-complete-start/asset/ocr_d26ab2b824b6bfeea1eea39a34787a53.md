![](bbox=[0.25, 0.1, 0.65, 0.3])

**FIGURE 4.5**
Result showing how overriding base class members behave

As you saw from the previous exercise, an overridden member is implicitly virtual and can be further overridden by subsequent derived classes. You did this when you implemented the override for Drive in the Car class, even though FourWheeledVehicle already overrode Drive. Normally this behavior is desirable; however, there might be times when you want to prevent it from occurring.

You can prevent further inheritance for a class member or a class by **sealing** it. To seal a class member, you include the sealed keyword in addition to the override keyword. To seal a class, you simply include the sealed keyword.

# **Sealing Classes**

Designing classes properly for inheritance can be a lot of work, so you have three choices:

+   * Leave the class unsealed but do the work to make it safely inheritable, which might end up being unnecessary if no one ever inherits from your class.
* Leave the class unsealed but don't do the work. This puts the burden on the consumer for understanding how your class can be safely extended.
* Seal the class. If you are reasonably certain no one will need to inherit from your class, it is probably the best option. It is always possible to unseal the class later, which should have no breaking impact on code that is already using it. Sealing a class also allows certain additional runtime optimizations to occur during JIT compilation.

**By the**
*Way*

# # Abstract Classes and Members

Although inheriting from a class provides a lot of benefit, there are times when you need to provide derived classes with a standard implementation and need to guarantee that a derived class provides an implementation for a particular property or method, or it simply makes sense to have a class that can have no instances. If you think back to the vehicle hierarchy, there are simply no objects that are “vehicles”