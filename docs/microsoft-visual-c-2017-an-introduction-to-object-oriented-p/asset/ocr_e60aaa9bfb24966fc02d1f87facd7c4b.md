When you create Carpet objects from the class in 9-14, each Carpet will have its own length, width, and area, but all Carpet objects will have the same MOTTO. The field MOTTO is preceded by the keyword const, meaning MOTTO is constant. That is, no program can change its value. Making a constant public does not violate information hiding in the way that making an object's data fields public programs that use this class cannot change the object's constant value.

When you define a named constant within a class, it is always static, even though you use the keyword static as a modifier. In other words, the field belongs to the entire class, not to any particular instance of the class. When you create a static field, only one copy is stored for the entire class, no matter how many objects you instantiate. When you use a static constant in a client class, you use the class name and dot rather than an object name, as in Carpet.MOTTO. Built-in C# classes contain useful named constants, such as Math.PI, which contains the value of pi. You do not create a Carpet object to use pi; therefore it is static.

Throughout this book, you have been using static to describe the Main() method of a class. You do not need to create an object of any class that contains a Main() method to be able to use Main().

Figure 9-15 shows a program that instantiates and uses a Carpet object, and Figure 9-16 shows the results when the program executes. Notice, although the output statements require an object to use the Width, Length, and Area properties, MOTTO is referenced using the class name only.

```
using static System.Console;
class TestCarpet
{
    static void Main()
    {
        Carpet aRug = new Carpet();
        aRug.Width = 12;
        aRug.Length = 14;
        Write("The {0}x{1}", aRug.Width, aRug.Length);
        WriteLine("has an area of {0}", aRug.Area);
        WriteLine("Our motto is: {0}", Carpet.MOTTO);
    }
}
```

Figure 9-15 The TestCarpet program