![](bbox=[0.13, 0.14, 0.55, 0.48])

FIGURE 8-9

Finally, a class may be sealed. A sealed class cannot be used as a base class, so no derived classes are possible.

C# provides a common base class for all objects called object (which is an alias for the System.Object class in the .NET Framework). You take a closer look at this class in Chapter 9.

> NOTE Interfaces, described earlier in this chapter, can also inherit from other interfaces. Unlike classes, interfaces can inherit from multiple base interfaces (in the same way that classes can support multiple interfaces).

# Polymorphism

One consequence of inheritance is that classes deriving from a base class have an overlap in the methods and properties that they expose. Because of this, it is often possible to treat objects instantiated from classes with a base type in common using identical syntax. For example, if a base class called Animal has a method called EatFood(), then the syntax for calling this method from the derived classes Cow and Chicken will be similar:

```
Cow myCow = new Cow();
Chicken myChicken = new Chicken();
myCow.EatFood();
myChicken.EatFood();
```

Polymorphism takes this a step further. You can assign a variable that is of a derived type to a variable of one of the base types, as shown here: