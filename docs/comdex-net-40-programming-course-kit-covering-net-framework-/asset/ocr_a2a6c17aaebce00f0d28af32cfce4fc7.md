```
~~~csharp
    }
    public partial class Rectangle
    {
        public void Area()
        {
            Console.WriteLine("Area of the rectangle: " + length * width);
        }
    }
    class Program
    {
        static void Main(string[] args)
        {
            Rectangle rect = new Rectangle(20, 10);
            rect.Area();
            Console.ReadLine();
        }
    }
}
~~~
```

The first highlighted code snippet in Listing 2.3 defines a class, named **Rectangle**. The **Rectangle** class is divided into two partial classes. In the first partial class, we have declared two variables, **length** and **width**, for the **Rectangle** class and defined a constructor to initialize these variables. In the second partial class, we have defined a method, **Area()**, for the **Rectangle** class. The **Area()** method calculates and displays the area of the rectangle, represented by an object of the **Rectangle** class, on the screen. In the second highlighted code snippet, we have created an object, **rect**, of the **Rectangle** class and used that object to call the **Area()** method of the **Rectangle** class.

+   8. Press the **F5** key on the keyboard to run the application. The output of the application appears, as shown in Fig.C#-2.3:

![](bbox=[0.404, 0.523, 0.603, 0.615])

Fig.C#-2.3

# ## Static Classes

Static classes are used to define methods that can be accessed without creating an instance of the class. The **static** keyword is used to define a class and its members as static. You can use the class name to access the members of a static class. Some important features of a static class are as follows:

+   - It can contain only static members
+   - It cannot be instantiated
+   - It cannot have instance constructors, which are constructors that are used to create and initialize member variables of an instance
+   - It cannot be inherited

When you declare a static class, you must remember that static classes cannot be instantiated. Declaring a static class is similar to creating a class that contains only static members and a private constructor. Static methods cannot call non-static methods directly. To call a non-static method from a static method, you need to create an object of the class in which the non-static method is defined. Similarly, non-static methods cannot call static methods directly. To call a static method from a non-static method, you need to use the name of the class in which the static method is defined. A static member can exist inside a static or a non-static class.

Perform the following steps to create static classes:

+   1. *Start* Visual Studio 2010.