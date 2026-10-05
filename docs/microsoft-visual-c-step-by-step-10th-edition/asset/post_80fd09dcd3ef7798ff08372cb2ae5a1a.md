
> Static methods are also called class methods. However, static fields aren't usually called class fields; they're just called static fields (or sometimes static variables).

## Creating a static field by using the const keyword

By prefixing the field with the `const` keyword, you can declare that a field is static but that its value never changes. The keyword `const` is short for constant. A const field doesn't use the `static` keyword in its declaration but is nevertheless static. However, for reasons that are beyond the scope of this book, you can declare a field as `const` only when the field is a numeric type (such as `int` or `double`), a string, or an enumeration. (You'll learn about enumerations in Chapter 9, "Creating value types with enumerations and structures.") For example, here's how the `Math` class declares `PI` as a `const` field:

Click here to view code image

```
class Math
{
  public const double PI = 3.1415926535897;
}
```

## Understanding static classes

Another feature of the C# language is the ability to declare a class as static. A static class can contain only static members. (All objects that you create by using the class share a single copy of these members.)

The purpose of a static class is purely to act as a holder of utility methods and fields. A static class cannot contain any instance data or methods, and it doesn't make sense to create an object from a static class using the `new` operator. In fact, you can't actually use `new` to create an instance of an object using a static class even if you want to. (The compiler will report an error if you try.) If you need to perform any initialization, a static class can have a default constructor as long as it is also declared as static. Any other types of constructor are illegal and will be reported as such by the compiler.

If you were defining your own version of the Math class, containing only static members, it could look like this:

Click here to view code image

```
public static class Math {
    public static double Sin(double x) {...}
    public static double Cos(double x) {...}
    public static double Sqrt(double x) {...}
}
```

> Note
 The real Math class is not defined this way because it actually does have instance methods.

## Static using statements

Whenever you call a static method or reference a static field, you must specify the class to which the method or field belongs, such as Math.Sqrt or Console.WriteLine. Static using statements enable you to bring a class into scope and omit the class name when accessing static members. They operate in much the same way as ordinary using statements that bring namespaces into scope. This example illustrates how to use them:

Click here to view code image

```
using static System.Math;
using static System.Console;
...
var root = Sqrt(99.9);
WriteLine($"The square root of {root}");
```

Note of the keyword static in the using statements. The example brings the static methods of the System.Math and System.Console classes into scope. (You must fully qualify the classes with their namespaces.) You can then simply call the Sqrt and WriteLine methods. The compiler determines which class each method belongs to.

Herein lies a potential maintenance issue. Although you're typing less code, you have to balance this with the additional effort required when someone else has to maintain your code, because it's no longer clear which class each belongs to. IntelliSense in Visual Studio helps to some extent, but to a developer reading through the code and trying to track down the cause of a bug, it can obfuscate matters. So, use static statements carefully. (My preferred style is not to use them, although you are free to make your own choice!)

In the final exercise in this chapter, you'll add a static field to the Point class and initialize the field to 0. You will increment this count in both constructors. Finally, you will write a public static method to return this private static field. With this field, you can discover how many Point objects you have created.

## To write static members and call static methods

- 1. In Visual Studio 2022, display the Point class in the Code and Text Editor window.
- 2. Add a private static field called oldCount of type int to the Point class immediately before the first constructor and initialize it, like this:

Click here to view code image

```
class Point
{
    private int x, y;
    private static int oldCount = 0;

    public Point()
    {
        ...
    }
}
```

> **Note**
> ---
> You can write the keywords private and static in any order when you declare a field such as oldCount. However, the preferred order is private first, static second.

- 3. Add a statement to both Point constructors to increment the objectCount field, as shown in bold type in the code example that follows.

The Point class should now look like this:

Click here to view code image

```
class Point
{
    private int x, y;
    private static int objectCount = 0;

    public Point()
    {
        this.x = -1;
        this.y = -1;
        objectCount++;
    }

    public Point(int x, int y)
    {
        this.x = x;
        this.y = y;
        objectCount++;
    }
}
```

Each time an object is created, its constructor is called. As long as you increment the objectCount in each constructor (including the default constructor), objectCount will hold the number of objects created so far. This strategy works only because objectCount is a shared static field. If objectCount was an instance field, each object would have its own objectCount field that would be set to 1.

The question is now this: How can users of the Point class find how many Point objects have been created? At the moment, the objectCount field is private and not available outside the class. A poor solution would be to make the objectCount field public. This strategy would break the encapsulation of the class, and you would then have no guarantee that the objectCount field's value was correct because anyone could change the value in the field. A much better idea is to provide a public static method that returns the value of the objectCount field. This is what you'll do.

- 4. Add a public static method to the end of Point class called ObjectCount that returns an int but does not take any parameters. This method should return the value of the objectCount field, as shown in bold type here:

Click here to view image

```
class Point
{
  public static int ObjectCount() => objectCount;
}
```

- 5. Display the Program class in the Code and Text Editor. Add a statement to the doWork method to write the value returned by ObjectCount, as shown in bold type here:

Click here to view image

```csharp
static void doWork()
{
    Console.WriteLine($"Number of objects: {Point.ObjectCount()}");
}
```

- 6. On the Debug menu, select Start Debugging. Confirm that the message "Number of objects: 2" is written to the console.

- 7. Press Enter to close the program and return to Visual Studio 2022.

## Anonymous classes

An anonymous class has no name. This sounds strange, but it's actually handy in situations that you'll see later in this book, especially using query expressions. (You'll learn about query expressions in Chapter 20, “Decoupling application logic and handling events.”) For now, you’ll have to take it on faith that they are useful.

You create an anonymous class simply by using the new keyword and a pair of braces defining the fields and values you want to, like this:

Click here to view code image

```csharp
var myAnonymousObject = new { Name = "John", Age = 47 };
```

This class contains public fields Name (initialized to the integer 47) and Age (initialized to "John") The compiler infers the types of the fields from the types of the data you specify to initialize them.

When you define an anonymous class, the compiler synthesizes its own name for the class, but it won’t tell you what it is. Well, if you don’t know the name of the class, how can you create an object of the appropriate type and assign an instance of the class to it? In the example shown earlier, what the type of the variable myAnonymousObject be? The answer is that you don’t know, and that is the point of anonymous classes! However, this isn’t a problem if you declare myAnonymousObject as an implicitly typed variable using the var keyword, like this:

Click here to view code image

```csharp
var myAnonymousObject = new { "John", Age = 47 };
```

Remember that the var keyword causes the compiler to create a variable of the same type as the expression used to initialize it. In this case, the type of the expression is whatever name the compiler happens to generate for the anonymous class.

You can access the fields in the object by using the familiar dot notation, as demonstrated here:

Click here to view code image

```csharp
Console.WriteLine("Name: {myAnonymousObject.Name} Age: {myAnonymousObject.Age}");
```

You can even create other instances of the same anonymous class but with different values, such as in the following:
