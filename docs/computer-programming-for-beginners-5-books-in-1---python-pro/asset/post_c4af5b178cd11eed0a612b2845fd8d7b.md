
A destructor is a useful tool for releasing the memory resources before leaving a program. You cannot overload or inherit a destructor. The following example demonstrates how to use a destructor:

```csharp
using System;
namespace ConstructorApplication {
  class Person {
    private double height;  // Height of a person

    public Person() {  // A constructor
      Console.WriteLine("We are creating an object!");
    }
    ~Person() {  // A destructor
      Console.WriteLine("We are deleting an object!");
    }
    public void setHeight( double heig ) {
      height = heig;
    }
    public double getHeight() {
      return height;
    }
    static void Main(string[] args) {
      Person p = new Person();
      // set the height of the person
      p.setHeight(7.0);
      Console.WriteLine("The height of the person is : {0}", p.getHeight());
    }
  }
}
```

Here is the output from the function:

![](img/239ff1e8a63502805c86c4dfbd71509a_562_0.png)

## Static Members

To define a class member as static, we use the *static* keyword. When a class member is declared as static, it means that regardless of the number of objects of the class that are created, there exists only one copy of the static member.

The use of the *static* keyword means that there is only one instance of a member existing in the class. We use this keyword when we need to declare constants since their values can be retrieved by invocation of the class without the creation of an instance of the same. We can initialize static variables outside a class definition or a member function. Static variables can also be initialized inside a class definition.

Let us demonstrate the use of static variables using an example:

```csharp
using System;
namespace StaticApp {
    class StaticVariables {
        public static int x;

        public void count() {
            x++;
        }
        public int getX() {
            return x;
        }
    }
    class StaticTester {
        static void Main(string[] args) {
            StaticVariables var1 = new StaticVariables();
            StaticVariables var2 = new StaticVariables();
            var1.count();
            var1.count();
            var1.count();
            var2.count();
            var2.count();
            var2.count();
            Console.WriteLine("Variable x for var1 is: {0}", var1.getX());
            Console.WriteLine("Variable x for var2 is: {0}", var2.getX());
            Console.ReadKey();
        }
    }
}
```

The code returns the following result:

![](img/239ff1e8a63502805c86c4dfbd71509a_563_0.png)

A member function can also be declared as static. Such a function will only be able to access static variables. Static functions exist even before the creation of the object. Static functions can be used as demonstrated in the following example:

```csharp
using System;
namespace StaticAppli {
    class StaticVariable {
        public static int x;
        public void count() {
            x++;
        }
        public static int getX() {
            return x;
        }
    }
    class StaticTester {
        static void Main(string[] args) {
            StaticVariable var = new StaticVariable();

            var.count();
            var.count();
            var.count();
            Console.WriteLine("Variable x is: {0}", StaticVariable.getX());
            Console.ReadKey();
        }
    }
}
```

The code will return the following:

![](img/239ff1e8a63502805c86c4dfbd71509a_564_0.png)

## Chapter 12: Structure

A structure in C# is a value type data type. With a structure, you can use a single variable to hold related data belonging to different data types. In C#, we use the *struct* keyword to create a structure.

Structures are used for tracking records. A good example is when you need to keep a record of all class students or all company employees. For the case of storing student records, some of the details that you may need to track, including the names, age, course, date of enrollment, date of completion, amount of fee paid, fee balance etc, guardian address and mobile phone number etc. All these details belong to different data types, meaning that you will be required to create a variable for each of them. However, by use of a structure, you can define a single variable and keep these details together as one.

Here is an example of declaring a structure:

```csharp
struct Employee{
    public string name;
    public string department;
    public string title;
    public int age;
    public double salary;
};
```

To initialize a struct, we can choose the *new* keyword or not. The members of a struct can be assigned values as shown below:

```csharp
using System;

public class MyStruct
{
    public static void Main()
    {
        Employee emp = new Employee();
        emp.name = "Nicholas Samuel";
        emp.department = "Computing";
```

Note that a struct is a value type, and this makes it faster when compared to a class object. This has made them good for use in game programming. However, one can more easily transfer a class object than a struct. This means that a struct should not be used when one is in need of transferring data to other classes.

Here is another example of a struct in C#:

```csharp
using System;
struct Cars {
    public string model;
    public int cc;
    public int passengers;
    public int year;
};
public class carStructure {
    public static void Main(string[] args) {
        Cars Premio;    /* Declare premio of type Car */
        Cars X6;    /* Declare X6 of type Car */
        /* premio specification */
        Premio.model = "Saloon";
        Premio.cc = 1800;
        Premio.passengers = 5;
        Premio.year = 2010;
        /* X6 specification */
        X6.model = "Saloon";
        X6.cc = 3500;
        X6.passengers = 5;
        X6.year = 2012;
        /* print premio info */
        Console.WriteLine("Premio model: {0}", Premio.model);
        Console.WriteLine("Premio CC : {0}", Premio.cc);
        Console.WriteLine("Premio passengers : {0}", Premio.passengers);
        Console.WriteLine("Premio year : {0}", Premio.year);
        /* print X6 info */
        Console.WriteLine("X6 model: {0}", X6.model);
        Console.WriteLine("X6 CC : {0}", X6.cc);
        Console.WriteLine("X6 passengers : {0}", X6.passengers);
        Console.WriteLine("X6 year :{0}", X6.year);
        Console.ReadKey();
    }
}
```

The code will return the following details¹³⁰:

![](img/239ff1e8a63502805c86c4dfbd71509a_568_0.png)

![](img/239ff1e8a63502805c86c4dfbd71509a_569_0.png)

We have created a single struct named *Cars*. In this structure, we have stored the two members, Premio and X6. These two instances are instances of the structure. The properties for these had been defined inside the structure. The two instances share properties, but these will take different values. We have then printed the values of these properties as shown in the above output.

### Characteristics of Structures

So far, you have known how to use structures and some of their characteristics. The structures in C# have a great difference from the structures supported in C and C++. C# structures have the features described below:

- Structures may have fields, indexers, methods, properties, operators and events.
- A structure can have defined constructors, not destructors. However, in a structure, we are not allowed to define a default constructor. The reason is that this is defined automatically and one cannot change it.
- A structure cannot inherit another structure or a class.
- With a structure, we can implement one or more interfaces.
- The members of a structure cannot be specified as virtual, abstract, or protected.
- After the creation of a Struct object via the *New* keyword, the struct object is created and the necessary constructor is called. Unlike classes, we can instantiate a struct without the use of the *New* keyword.
- If we don’t use the New operator, the fields will not be assigned and it will not be possible to use the object until an assignment has been done to all the fields.

### Struct vs. Class

Here are the differences between Structs and Classes:

- A Struct is explained as a value type. On the other side, a class is defined as a reference type.
- Structs don’t support inheritance. Classes do.
- A Struct cannot have a default constructor. A class can.

Let us create an example in relation to the above differences:

```csharp
using System;
struct Cars {
    private string model;
    private int cc;
    private int passengers;
    private int year;
    public void getValues(string m, int c, int p, int yr) {
        model = m;
        cc = c;
        passengers = p;
        year = yr;
```
