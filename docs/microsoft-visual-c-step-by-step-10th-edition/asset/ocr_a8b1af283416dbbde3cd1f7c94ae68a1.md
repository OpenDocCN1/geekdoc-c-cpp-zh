```
abstract class GrazingMammal : Mammal, IGrazable
{
    public abstract void DigestGrass();
    ...\n}
```

> Note
at first glance, an abstract class and an interface with default method implementations may appear to be similar, but they are fundamentally different beasts. An abstract class can contain fields, constructors, a destructor, private methods, and other members that you would typically find in any class. An interface is simply a specification of what a class should look like.

# Sealed classes

Using inheritance is not always easy and requires forethought. If you create an interface or an abstract class, you are knowingly writing something that will be inherited from the future. The trouble is that predicting the future is a difficult business. With practice and experience, you can develop the skills to craft a flexible, easy-to-use hierarchy of interfaces, abstract classes, and classes, but it takes effort as well as a solid understanding of the problem that you're modeling. To put it another way, unless you consciously design a class with the intention of using it as a base class, it's extremely unlikely that it will function well as a base class.

With C#, you can use the sealed keyword to prevent a class from being used as a base class if you decide that it should not be. For example, in the following code, if any class attempts to use Horse as a base class, a compile-time error will be generated:

Click here to view code image

```
sealed class Horse : GrazingMammal, ILandBound
{
    ...
```