
## Note

Be warned that this assignment statement might not accomplish what you expect. You’ll learn more about assigning object variables in Chapter 8.

There are quite a few restrictions on the contents of an anonymous class. For example, anonymous classes can contain only public fields, the fields must all be initialized, they cannot be static, and you cannot define any methods for them. You will use anonymous classes periodically throughout this book and learn more about them as you do so.

## Summary

In this chapter, you saw how to define new classes. You learned that by default the fields and methods of a class are private and inaccessible to code outside the class, but you can use the *public* keyword to expose fields and methods to the outside world. You saw how to use the *new* keyword to create a new instance of a class and how to define constructors that can initialize class instances. Finally, you saw how to implement static fields and methods to provide data and operations that are independent of any specific instance of a class.

- If you want to continue to the next chapter, keep Visual Studio 2015 running and turn to Chapter 8.
- If you want to exit Visual Studio 2015 now, on the File menu, click Exit. If you see a Save dialog box, click Yes and save the project.

## Quick reference

| To | Do this |
|---|---|
| Declare a class | Write the keyword *class*, followed by the name of the class, followed by opening and closing braces. The methods and fields of the class are declared between the opening and closing braces. For example:
```
class Point
{
    ...
}
``` |
| Declare a constructor | Write a method whose name is the same as the name of the class and that has no return type (not even *void*). For example:
```
class Point
{
    public Point(int x, int y)
    {
        ...
    }
}
``` |
| Call a constructor | Use the *new* keyword and specify the constructor with an appropriate set of parameters. For example:
```
Point origin = new Point(0, 0);
``` |
| Declare a static method | Write the keyword *static* before the declaration of the method. For example:
```
class Point
{
    public static int ObjectCount()
    {
        ...
    }
}
``` |
| Call a static method | Write the name of the class, followed by a period, followed by the name of the method. For example:
```
int pointsCreatedSoFar = Point.ObjectCount();
``` |
| Declare a static field | Use the keyword *static* before the type of the field. For example:
```
class Point
{
    ...
    private static int objectCount;
}
``` |
| Declare a const field | Write the keyword *const* before the declaration of the field and omit the *static* keyword. For example:
```
class Math
{
    ...
    public const double PI = ...;
}
``` |
| Access a static field | Write the name of the class, followed by a period, followed by the name of the static field. For example:
```
double area = Math.PI * radius * radius;
``` |

## Chapter 8. Understanding values and references

After completing this chapter, you will be able to:

- Explain the differences between a value type and a reference type.
- Modify the way in which arguments are passed as method parameters by using the ref and out keywords.
- Convert a value into a reference by using boxing.
- Convert a reference back to a value by using unboxing and casting.

Chapter 7, “Creating and managing classes and objects,” demonstrates how to declare your own classes and how to create objects by using the new keyword. That chapter also shows you how to initialize an object by using a constructor. In this chapter, you will learn how the characteristics of the primitive types—such as int, double, and char—differ from the characteristics of class types.

## Copying value type variables and classes

Most of the primitive types built into C#, such as int, float, double, and char (but not string, for reasons that will be covered shortly) are collectively called value types. These types have a fixed size, and when you declare a variable as a value type, the compiler generates code that allocates a block of memory big enough to hold a corresponding value. For example, declaring an int variable causes the compiler to allocate 4 bytes of memory (32 bits) to hold the integer value. A statement that assigns a value (such as 42) to the int causes the value to be copied into this block of memory.

Class types such as Circle (described in Chapter 7) are handled differently. When you declare a Circle variable, the compiler does not generate code that allocates a block of memory big enough to hold a Circle; all it does is allot a small piece of memory that can potentially hold the address of (or a reference to) another block of memory containing a Circle. (An address specifies the location of an item in memory.) The memory for the actual Circle object is allocated only when the new keyword is used to create the object. A class is an example of a reference type. Reference types hold references to blocks of memory. To write effective C# programs that make full use of the Microsoft .NET Framework, you need to understand the difference between value types and reference types.

## Note

The string type in C# is actually a class. This is because there is no standard size for a string (different strings can contain different numbers of characters), and allocating memory for a string dynamically when the program runs is far more efficient than doing so statically at compile time. The description in this chapter of reference types such as classes applies to the string type as well. In fact, the string keyword in C# is just an alias for the System.String class.

Consider a situation in which you declare a variable named i as an int and assign it the value 42. If you declare another variable called copyi as an int and then assign i to copyi, copyi will hold the same value as i (42). However, even though copyi and i happen to hold the same value, two blocks of memory contain the value 42: one block for i and the other block for copyi. If you modify the value of i, the value of copyi does not change. Let’s see this in code:

Click here to view code image

```
int i = 42;      // declare and initialize i
int copyi = i; /* copyi contains a copy of the data in i:
                  i and copyi both contain the value 42 */
i++;             /* incrementing i has no effect on copyi;
                  i now contains 43, but copyi still contains 42 */
```

The effect of declaring a variable c as a class type, such as Circle, is very different. When you declare c as a Circle, c can refer to a Circle object; the actual value held by c is the address of a Circle object in memory. If you declare an additional variable named refc (also as a Circle) and you assign c to refc, refc will have a copy of the same address as c; in other words, there is only one Circle object, and both refc and c now refer to it. Here’s the example in code:

```
Circle c = new Circle(42);
Circle refc = c;
```

The following illustration shows both examples. The at sign (@) in the Circle objects represents a reference holding an address in memory:

![](img/16f6e3fe08f01ddadb2741a92c392b0e_231_0.png)

![](img/16f6e3fe08f01ddadb2741a92c392b0e_231_1.png)

This difference is very important. In particular, it means that the behavior of method parameters depends on whether they are value types or reference types. You’ll explore this difference in the next exercise.

## Copying reference types and data privacy

If you actually want to copy the contents of a Circle object, c, into a different Circle object, refc, instead of just copying the reference, you must make refc refer to a new instance of the Circle class and then copy the data, field by field, from c into refc, like this:

Click here to view code image

```
Circle refc = new Circle();
refc.radius = c.radius;    // Don't try this
```

However, if any members of the Circle class are private (like the radius field), you will not be able to copy this data. Instead, you can make the data in the private fields accessible by exposing them as properties and then use these properties to read the data from c and copy it into refc. You will learn how to do this in Chapter 15, “Implementing properties to access fields.”

Alternatively, a class could provide a Clone method that returns another instance of the same class but populated with the same data. The Clone method would have access to the private data in an object and could copy this data directly to another instance of the same class. For example, the
