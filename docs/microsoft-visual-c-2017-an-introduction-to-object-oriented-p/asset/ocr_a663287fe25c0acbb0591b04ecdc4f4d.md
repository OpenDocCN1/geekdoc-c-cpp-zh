```
using static System.Console;
class DemoAnimals2
{
    static void Main()
    {
        Dog Spot = new Dog("Spot");
        Cat puff = new Cat("Puff");
        DisplayAnimal(spot);
        DisplayAnimal(puff);
    }
    public static void DisplayAnimal(Animal creature)
    {
        WriteLine(creature.Name + " says " + creature.Speak());
    }
}
```

**Figure 10-35** The DemoAnimals2 program

# TWO TRUTHS & A LIE

# Creating and Using Abstract Classes

+   1. An abstract class is one from which you cannot create concrete objects.
2. Unlike regular classes, abstract classes cannot contain methods.
3. When a base class contains an abstract method, the descendants of the base class must override the abstract method or declare the overriding method to be.

> derived.
abstract classes simply to provide a base class from which other objects may
ininstances of abstract classes by using the new operator. However, you create
can contain data fields and methods. The difference is that you cannot create
The false statement is #2. Abstract classes are like regular classes in that they are

# Creating and Using Interfaces

Object-oriented programming languages, notably C+, allow a subclass to inherit from more than one parent class. For example, you might create an Employee class that contains data fields pertaining to each employee in your organization. You might also create a Product class that holds information about each product your organization manufactures. When you create a Patent class for each product that your company holds a patent, you might want to include product information as well as information about the who was responsible for the invention. In this situation, it would be convenient to inherit fields and methods from