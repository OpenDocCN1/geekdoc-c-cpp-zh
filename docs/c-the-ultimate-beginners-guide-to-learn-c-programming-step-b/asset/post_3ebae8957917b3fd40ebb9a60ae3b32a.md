
```csharp
namespace ConstructorApplication {
    class Person {
        private double height;  // height of the person

        public Person() {
            Console.WriteLine("We are creating an object");
        }
        public void setHeight( double heig ) {
            height = heig;
        }
        public double getHeight() {
            return height;
        }
        static void Main(string[] args) {
            Person p = new Person();
            // set the person's height
            p.setHeight(7.0);
            Console.WriteLine("The height of the person is: {0}", p.getHeight());
            Console.ReadKey();
        }
    }
}
```

The code should return the following:

```text
We are creating an object
The height of the person is: 7
```

A default constructor has no parameters, but it is possible to add parameters to a constructor. Such a constructor is known as a *parameterized constructor*. With such a technique, it is possible for one to assign an initial value to an object during the time of its creation. Here is an example:

```csharp
using System;
namespace ConstructorApplication {
    class Person {
        private double height;    // Height of the person
        public Person(double heig) {    // A parameterized constructor
            Console.WriteLine("We are creating an object, height = {0}", heig);
            height = heig;
        }
        public void setHeight( double heig) {
            height = heig;
        }
        public double getHeight() {
            return height;
        }
        static void Main(string[] args) {
            Person p = new Person(8.0);
            Console.WriteLine("The height of the person is : {0}", p.getHeight());
            // set the height
            p.setHeight(7.0);
            Console.WriteLine("The height of the person is : {0}", p.getHeight());
            Console.ReadKey();
        }
    }
}
```

Here is the output from the code:

```text
We are creating an object, height = 8
The height of the person is : 8
The height of the person is : 7
```

## Destructors

A destructor refers to a special member function of a class that is run anytime an object of the class goes out of scope. A destructor takes the same name as a class but it should be preceded by a tilde (~). A destructor cannot take parameters neither can it return a value.

A destructor is a useful tool for releasing the memory resources before leaving a program. You can overload or inherit a destructor. The following example demonstrates how to use a destructor:

```csharp
using System;

namespace ConstructorApplication {
    class Person {
        private double height;  // Height of a person

        public Person() {  // A constructor
            Console.WriteLine("We are creating an object");
        }

        ~Person() {  // A destructor
            Console.WriteLine("We are deleting an object");
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

```text
We are creating an object
The height of the person is : 7
We are deleting an object
```

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

```text
Variable x for var1 is: 6
Variable x for var2 is: 6
```

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

```text
Variable x is: 3
```

## Chapter 12: Structure

A structure in C# is a value type data type. With a structure, you can use a single variable to hold related data belonging to different data types. In C#, we use the *struct* keyword to create a structure[32].

Structures are used for tracking records. A good example is when you need to keep a record of all class students or all company employees. For the case of storing student records, some of the details that you may need to track including the names, age, course, date of enrollment, date of completion, amount of fee paid, fee balance etc, guardian address and mobile phone number etc. All these details belong to different data types, meaning that you will be required to create a variable for each of them. However, by use of a structure, you can define a single variable and keep these details together as one.

Here is an example of declaring a structure[33]:

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
        emp.age = 26;
        emp.salary = 5000;
        Console.WriteLine(emp.name);
        Console.WriteLine(emp.department);
        Console.WriteLine(emp.age);
        Console.WriteLine(emp.salary);
    }
}
```

```csharp
public struct Employee
{
    public string name { get; set; }
    public string department { get; set; }
    public string title { get; set; }
    public int age { get; set; }
    public double salary { get; set; }
}
```

The code gives the following result:

```text
Nicholas Samuel
Computing
26
5000
```

The struct named *Employee* was defined using the struct keyword. The various details of this struct have been declared within this. At the top of the class, we created an instance of this struct and we gave it the name *emp*. This instance has been used to access the various attributes of the struct for display on the screen.

Note that a struct is a value type, and this makes it faster when compared to a class object. This has made them good for use in game programming. However, one can
