
In Listing 4.7, we have created one constructor named Program (you already know that the constructor has the same name as the class). In the Main() method, we have initialized the constructor and passed the parameters required to initialize the values of different variables. Then, we have accessed the area() method to calculate the area of the rectangle.

5. Press the F5 key to run the ConstructorApp application.

The output of the application appears, as shown in Fig.C#4.6:

![](img/2db4b8b2cb67e7ccc52477a61fe289ab_114_0.png)

Fig.C#4.6

Next, let's discuss the static constructors.

## Static Constructors

A static constructor is the one that can be used to access the static members of a class and therefore, a static constructor is often used to initialize the static members of a class. You can also use a static constructor when you need to perform any particular task that has to be performed just once. A static constructor is automatically invoked for the first time a class loads into the memory and there can be only one static constructor in a class. The syntax to define a static constructor is as follows:

```
public class StaticConstructorClass
{
    static StaticConstructorClass()
    {
        // some code
    }
}
```

The preceding code snippet shows that the name of a static constructor is not prefixed by an access modifier; instead, it is preceded by the keyword static. The following are some of the main properties of a static constructor:

- A static constructor's name is neither prefixed by any access modifier nor does it take any arguments
- It is automatically invoked for the first time to initialize a class even before any of its instances has been created or any other static data member is referenced
- It cannot be called directly
- A user has no control over the execution of a static constructor in a program

Let's perform the following steps to create an application named StaticConstructor to see how a static constructor is created and invoked:

- 1. Repeat steps 1 to 3 discussed while creating the CreatingMethod application in the Defining a Method section of this chapter.
- 2. Enter StaticConstructor in the Name text box to specify the name of the application, and specify an appropriate location for the application in the Location combo box.
- 3. Click the OK button. The StaticConstructor application is created.
- 4. In the Program.cs file, add the highlighted code given in Listing 4.8:

Listing 4.8: Creating a Static Constructor

```
namespace StaticConstructor
{
    public class StaticTest
    {
        static StaticTest()
        {
            Console.WriteLine("Executing the Static Constructor");
        }
        public StaticTest()
        {
            Console.WriteLine("Executing a non-static Constructor");
        }
    }
    class Program
    {
        static void Main(string[] args)
        {
            StaticTest st = new StaticTest();
            Console.ReadLine();
        }
    }
}
```

In Listing 4.8, we have created a static constructor and a non-static constructor. Inside the Main() method, the non-static constructor of the class StaticTest is invoked automatically when an object of that class is created using the new operator. Note that we have not made any call to the static constructor since a static constructor is automatically invoked the first time a class loads into the memory.

5. Press the F5 key to run the StaticConstructor application.

The output of the application appears, as shown in Fig.C#4.7:

![](img/2db4b8b2cb67e7ccc52477a61fe289ab_115_0.png)

In Fig.C#4.7, you can see that when the class StaticTest is loaded for the first time in the memory, the static constructor executes first, irrespective of the fact that the class already has a non-static constructor defined. After the static constructor is executed, the non-static constructor of the class StaticTest executes.

## Instance Constructors

The constructors that are used to create and initialize the instance variables of a class using the new operator are known as instance constructors. The following code snippet illustrates how to define an instance constructor:

```
public class Numbers
{
    int a,b;
    public Numbers() // instance constructor
    {
        a = 0;
        b = 0;
    }
}
```

In the preceding code snippet, an instance constructor is defined. It is invoked whenever an object of the class Numbers is created. The constructor in the preceding code snippet takes no arguments; however, we can add such constructors to our code that take some arguments. Such constructors are known as parameterized constructors. For example, we can add a parameterized constructor to the class Numbers, as shown in the following code snippet:

```
public Numbers(int a, int b) // parameterized constructor
{
    this.a = a;
    this.b = b;
}
```

The instances of a class can be created either by invoking the instance constructor or by calling the parameterized constructor or both, as shown in the following code snippet:

```
Numbers num1 = new Numbers(); //default constructor
Numbers num2 = new Numbers(1, 2); //parameterized constructor
```

When no constructor for a class has been defined explicitly by the programmer in the source code, the default constructor for that class is automatically called and the value of the instance variables is initialized to their default values. Now, let’s perform the following steps to create an application named **ConstructorTypes** to understand how the default and parameterized constructors work:

- 1. *Repeat* steps 1 to 3 discussed while creating the **CreatingMethod** application in the **Defining a Method** section of this chapter.
- 2. *Enter* **ConstructorTypes** in the **Name** text box to specify the name of the application, and specify an appropriate location for the application in the **Location** combo box.
- 3. *Click* the **OK** button. The **ConstructorTypes** application is created.
- 4. In the **Program.cs** file, *add* the highlighted code given in Listing 4.9:

### Listing 4.9: Demonstrating an Instance and Parameterized Constructor

```
namespace ConstructorTypes
{
    public class Numbers
    {
        int a, b;
        public Numbers() // instance constructor
        {
            a = 0;
            b = 0;
        }
        public Numbers(int a, int b) //parameterized constructor
        {
            this.a = a;
            this.b = b;
        }
        public void ShowNumbers()
        {
            Console.WriteLine("The numbers are {0} and {1}", a,b);
        }
    }
    public class Program
    {
        public static void Main(string[] args)
        {
            Numbers num1 = new Numbers();
            Numbers num2 = new Numbers(2, 3);
            num1.ShowNumbers();
            num2.ShowNumbers();
            Console.ReadLine();
        }
    }
}
```

In Listing 4.9, two integer instance variables, a and b, are declared. An instance constructor is defined as that does not take any parameters. A parameterized constructor is also defined as that takes two parameters. In the Main() method, we have invoked both the constructors. Thereafter, the ShowNumbers() method is invoked to display the values of instance variables, a and b, in the objects, num1 and num2, of the class Numbers.

5. Press the F5 key to run the ConstructorTypes application.
The output of the application appears, as shown in Fig.C#4.8:

![](img/2db4b8b2cb67e7ccc52477a61fe289ab_117_0.png)

Fig.C#4.8

In Fig.C#4.8, when the instance constructor is called, the instance variables a and b are initialized to 0; on the other hand, on invoking the parameterized constructor, the values of the instance variables are initialized as per the arguments passed to the constructor.

In this section, you have learned how to create objects using constructors. However, there may be times when you need to release these objects. The next section discusses how you can free unused objects.

## Garbage Collection in C# 2010

The garbage collection feature of .NET Framework is responsible for the management of resources such as memory. It is due to this memory management aspect of .NET Framework that a .NET application developer need not worry about allocating and then releasing memory for objects in an application. In other words, it can be said that with the help of this feature, the .NET developers do not require to write code to perform memory management tasks. Therefore, the automatic garbage collection mechanism in C# helps prevent issues, such as memory leaks caused by forgetting to free an unused object, null pointer exceptions that are caused when an attempt is made to access the memory of an object that has long been freed, and many more.

In C#, the garbage collection mechanism is managed by common language runtime (CLR). As long as there is free space in the managed heap, new objects are automatically allocated memory by CLR. Therefore, the garbage collection is performed periodically by the Garbage Collector (GC) to reclaim the memory from any unreferenced objects and to make it available for subsequent allocation to some other object. The garbage collection mechanism also enforces memory safety, which means that the contents of one object cannot be accessed by some other object.

As stated earlier, garbage collection is performed periodically for .NET applications; yet there might be times when you need to force the GC to deallocate memory from any unused object. For this purpose, you can call the GC.Collect() method. This method causes an immediate garbage collection on objects of all generations. The syntax to call the GC.Collect() method to reclaim inaccessible memory from objects of generation 0 is as follows:

```
GC.Collect();
```

In .NET Framework 4.0, support for background garbage collection has been added as opposed to the concurrent garbage collection feature that was supported in the earlier versions of .NET Framework. This background garbage collection feature means that garbage collection can be simultaneously performed on generation 0 and generation 1 objects while the garbage collection is being performed on generation 2 objects.

### Note

> The .NET GC is a generational garbage collector. In fact, the managed heap has been partitioned into three generations, which are known as generation 0, generation 1, and generation 2. A newly created object is stored in the generation 0 by the GC. As the memory is finite and there may soon come a time when there is no free space available in the managed heap; therefore, the GC will deallocate objects stored in generation 0. Those objects that survive the first pass of garbage collection are then moved on to generation 1. The generation 2 consists of those objects that survive the first two garbage collection passes. The objects stored in generation 2 are also known as long-lived objects.
