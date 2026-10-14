
method is an extension method for the int type, and another ordinary int parameter named baseToConvertTo.

The method will convert the value in i to the base indicated by baseToConvertTo. The method should return an int containing the converted value.

The ConvertToBase method should look like this:

Click here to view code image

```
static class Util
{
    public static int ConvertToBase(this int i, int baseToConvertTo)
    {
    }
}
```

4. Add an if statement to the ConvertToBase method that checks that the value of the baseToConvertTo parameter is between 2 and 10.

The algorithm used by this exercise does not work reliably outside this range of values. Throw an ArgumentException exception with a suitable message if the value of baseToConvertTo is outside this range.

The ConvertToBase method should look like this:

Click here to view code image

```
public static int ConvertToBase(this int i, int baseToConvertTo)
{
    if (baseToConvertTo < 2 || baseToConvertTo > 10)
    {
        throw new ArgumentException("Value cannot be converted to base " + baseToConvertTo.ToString());
    }
}
```

5. Add the following statements shown in bold to the ConvertToBase method, after the statement that throws the ArgumentException exception.

This code implements a well-known algorithm that converts a number from base 10 to a different number base. (Chapter 5, “Using compound assignment and iteration statements,” presents a version of this algorithm for converting a decimal number to octal.)

Click here to view code image

```
public static int ConvertToBase(this int i, int baseToConvertTo)
{
    ...
    int result = 0;
    int iterations = 0;
    do
```
```
{
    int nextDigit = i % baseToConvertTo;
    i /= baseToConvertTo;
    result += nextDigit * (int)Math.Pow(10, iterations);
    iterations++;
}
while (i != 0);

return result;
}
```

6. Display the Program.cs file in the Code and Text Editor window.

7. Add the following using directive after the using System; directive at the top of the file:

```
using Extensions;
```

This statement brings the namespace containing the Util class into scope. The ConvertToBase extension method will not be visible in the Program.cs file if you do not perform this task.

8. Add the following statements shown in bold to the doWork method of the Program class, replacing the // TODO: comment:

Click here to view code image

```
static void doWork()
{
    int x = 591;
    for (int i = 2; i <= 10; i++)
    {
        Console.WriteLine($"{x} in base {i} is {x.ConvertToBase(i)}");
    }
}
```

This code creates an int named x and sets it to the value 591. (You can pick any integer value you want.) The code then uses a loop to print out the value 591 in all number bases between 2 and 10. Notice that ConvertToBase appears as an extension method in IntelliSense when you type the period (.) after x in the Console.WriteLine statement.

9. On the Debug menu, click Start Without Debugging. Confirm that the program displays messages to the console showing the value 591 in the different number bases, like this:

![](img/16f6e3fe08f01ddadb2741a92c392b0e_341_0.png)

10. Press Enter to close the program and return to Visual Studio 2015.

## Summary

In this chapter, you learned how to use inheritance to define a hierarchy of classes, and you should now understand how to override inherited methods and implement virtual methods. You also learned how to add an extension method to an existing type.

+   If you want to continue to the next chapter, keep Visual Studio 2015 running and turn to Chapter 13.
+   If you want to exit Visual Studio 2015 now, on the File menu, click Exit. If you see a Save dialog box, click Yes and save the project.

## Quick reference

| To | Do this |
|---|---|
| Create a derived class from a base class | Declare the new class name followed by a colon and the name of the base class. For example:
```
class DerivedClass : BaseClass
{
    ...
}
``` |
| Call a base-class constructor as part of the constructor for an inheriting class | Suffix the definition of the constructor with a call to *base*, before the body of the derived-class constructor, and provide any necessary parameters to the *base* constructor. For example:
```
class DerivedClass : BaseClass
{
    ...
    public DerivedClass(int x) : base(x)
    {
        ...
    }
    ...
}
``` |
| Declare a virtual method | Use the *virtual* keyword when declaring the method. For example:
```
class Mammal
{
    public virtual void Breathe()
    {
        ...
    }
    ...
}
``` |
| Implement a method in a derived class that overrides an inherited virtual method | Use the *override* keyword when declaring the method in the derived class. For example:
```
class Whale : Mammal
{
    public override void Breathe()
    {
        ...
    }
    ...
}
``` |
| Define an extension method for a type | Add a static public method to a static class. The first parameter must be of the type being extended, preceded by the *this* keyword. For example:
```
static class Util
{
    public static int Negate(this int i)
    {
        return -i;
    }
}
``` |

## Chapter 13. Creating interfaces and defining abstract classes

After completing this chapter, you will be able to:

+   - Define an interface specifying the signatures and return types of methods.
+   - Implement an interface in a structure or class.
+   - Reference a class through an interface.
+   - Capture common implementation details in an abstract class.
+   - Implement sealed classes that cannot be used to derive new classes.

Inheriting from a class is a powerful mechanism, but the real power of inheritance comes from inheriting from an interface. An interface does not contain any code or data; it just specifies the methods and properties that a class that inherits from the interface must provide. By using an interface, you can completely separate the names and signatures of the methods of a class from the method’s implementation.

Abstract classes are similar to interfaces in many ways, except that abstract classes can contain code and data. However, you can specify certain methods of an abstract class as virtual so that a class that inherits from the abstract class can optionally provide its own implementation of these methods. You frequently use abstract classes with interfaces, and together they provide a key technique with which you can build extensible programming frameworks, as you will discover in this chapter.

### Understanding interfaces

Suppose that you want to define a new class in which you can store collections of objects, a bit like you would use an array. However, unlike with an array, you want to provide a method named RetrieveInOrder to enable applications to retrieve objects in a sequence that depends on the type of object the collection contains. (With an ordinary array, you can iterate through its contents, and by default you retrieve items according to their index.) For example, if the collection holds alphanumeric objects such as strings, the collection should enable an application to retrieve these strings in sequence according to the collating sequence of the computer, and if the collection holds numeric objects such as integers, the collection should enable the application to retrieve objects in numerical order.

When you define the collection class, you do not want to restrict the types of objects that it can hold (the objects can even be class or structure types), and consequently you don’t know how to order these objects. So, how do you provide the collection class with a method that sorts objects whose types you do not know when you actually write the collection class? At first glance, this problem seems
similar to the *ToString* problem described in Chapter 12, “Working with inheritance,” which could be resolved by declaring a virtual method that subclasses of your collection class can override. However, any similarity is misleading. There is no inheritance relationship between the collection class and the objects that it holds, so a virtual method would not be of much use. If you think for a moment, the problem is that the way in which the objects in the collection should be ordered is dependent on the type of the object in the collection and not on the collection itself. The solution is to require that all the objects provide a method, such as the *CompareTo* method shown in the following example, that the *RetrieveInOrder* method of the collection can call, making it possible for the collection to compare these objects with one another:

Click here to view code image

```
int CompareTo(object obj)
{
    // return 0 if this instance is equal to obj
    // return < 0 if this instance is less than obj
    // return > 0 if this instance is greater than obj
    ...
}
```

You can define an interface for collectable objects that includes the *CompareTo* method and specify that the collection class can contain only classes that implement this interface. In this way, an interface is similar to a contract. If a class implements an interface, the interface guarantees that the class contains all the methods specified in the interface. This mechanism ensures that you will be able to call the *CompareTo* method on all objects in the collection and sort them.

Using interfaces, you can truly separate the “what” from the “how.” An interface gives you only the name, return type, and parameters of the method. Exactly how the method is implemented is not a concern of the interface. The interface describes the functionality that a class should provide but not how this functionality is implemented.

### Defining an interface

Defining an interface is syntactically similar to defining a class, except that you use the *interface* keyword instead of the *class* keyword. Within the interface, you declare methods exactly as in a class or a structure, except that you never specify an access modifier (*public*, *private*, or *protected*). Additionally, the methods in an interface have no implementation; they are simply declarations, and all types that implement the interface must provide their own implementations. Consequently, you replace the method body with a semicolon. Here is an example:

Click here to view code image

```
interface IComparable
```
