
```csharp
Console.WriteLine ( x );
}
```

## 12.40 Comment on the following code:

```csharp
class AB
{
    private int number;
    public int Number
    {
        get { return number;}
    }
    public int Number
    {
        set {number = value;}
    }
}
```

## 12.41 Consider the following code:

```csharp
class Product
{
    public static void Main ( )
    {
        int x = 10, y = 20;
        Console.WriteLine (mul (x, y));
    }
    int mul (int a, int b)
    {
        return (a*b);
    }
}
```

Will it compile? If not, why?

## 12.42 What is the use of the following code?

```csharp
class Student
{
    static int m = 0;
    public Student ()
    { m ++;}
    ...
    ...
}
```

## 12.43 Will the following code compile? If no, why?

```csharp
class A
{
    public static void Main ( )
    {
        Test t;
        T.Print();
    }
}
class Test
```

## Debugging Exercises

12.1 Find syntax errors in the following program.

```csharp
using System;
using System.Collections.Generic;
using System.Text;
namespace DebugApp1_chap12
{
    class Program
    {
        static void Main(string[] args)
        {
            Name nm = new Name();
            nm.Name1 = "Steve";
            nm.Address = "Washington";
            nm.ShowInfo();
            Console.ReadLine();
        }
    }
class Name
{
    public string Name1;
    public string Address;
    public void ShowInfo()
    {
        Console.WriteLine("{0} is in city {1}", + Name1, + Address);
    }
}
}
```

12.2 Debug the program given below.

```csharp
using System;
using System.Collections.Generic;
using System.Text;
namespace debugApp2_chap12
{
    class Program
    {
        static void Main(string[] args)
        {
            Name obj = new Name();
            obj.showInfo();
        }
    }
}
```

```csharp
}
void Display()
{
    Console.WriteLine(a + b);
}
}
class Program
{
    static void Main(string[] args)
    {
        Class2 cl = new Class2();
        Console.Write("The output is : ");
        cl.Display();
    }
}
}
```

## Programming Exercises

- 12.1 Create a class named Number to hold one integer value. Include a constructor to display the message "object is created" and a destructor to display the message "object is destroyed". Write a program to demonstrate the creation and destruction of Number objects.

- 12.2 Rewrite the program in Exercise 12.1 by adding a Set method to provide a value to the data member and a Get method to display the value stored in the object. Demonstrate your program by storing an integer value, say 2002, and display the same.

- 12.3 Rewrite the program in Exercise 12.2 by replacing the Set method by a constructor.

- 12.4 Rewrite the program in Exercise 12.2 by replacing the Set and Get methods by a property.

- 12.5 Create a class named Integer to hold two integer values. Design a method Swap that could take two integer objects as parameters and swap their contents. Write a Main program to implement the class Integer and the method Swap.

- 12.6 Design a class named Date with the following members:
  - Data members day, month and year
  - A constructor to provide values to the data members (using three parameters)
  - A method to display the date in the format day/month/year (Example: 15/8/1945 for August 15, 1945)
  Write a program to implement the class Date.

- 12.7 Add to the class designed in Exercise 12.6 another constructor which takes only one parameter that represents the date in the form of a long integer, like 19450815 for the date 15/8/1945 and assigns suitable values for the year, month and day members. Also modify the Main program to demonstrate the use of both the constructors. Use a suitable algorithm to convert the long integer 19450815 into year, month and day.

- 12.8 Define a Time class containing the following members:
  - Two integer data members minutes and hours
  - Two overloaded constructors
  - One method to display the class data members
  One of the constructors take two integer parameters to assign values to two data members and the other constructor takes one integer parameter representing total number of minutes and converts it into hours and minutes
  Write a complete program to verify the operation of the constructors and the method.

## 12.9 Add the following two methods to the Time class defined in Exercise 12.8

- Increment ( ) method that increments time by 1 minute
- Decrement ( ) method that decrements time by 1 minute

Test your methods to ensure that they perform correctly the intended operations.

## 12.10 Design a class to represent a bank account. Include the following members:

Data members

- Name of the depositor
- Account number
- Type of account
- Balance amount in the account

Methods

- To assign initial values
- To deposit an amount
- To withdraw an amount after checking balance
- To display the name and balance

Write a program to demonstrate the working of the various class members.

## 12.11 Write a class to represent a vector (a series of integer values). Include constructors and methods to perform the following tasks.

- To create the vector
- To modify the value of a given element
- To multiply by a scalar value
- To display the vector in the form (10, 20.....)

Write a program to test your class.

## 12.12 Modify the class and the program of Exercise 12.10 for handling 10 customers.

## 12.13 Modify the class and the program of Exercise 12.11 such that the program would be able to add two vectors and display the resultant vector.

## 12.14 A common use of static member variable is to keep track of objects that currently exist for a class.

Write a program to illustrate this feature.

## 12.15 Create two classes DM and DB which store the values of distances. DM stores the distances in metres and centimeters and DB in feet and inches. Write a program that can read values for the class objects and add one object of DM with another object of DB. The program should display the result in the format of feet and inches or metres and centimeters as required.

## 12.16 A book shop maintains the inventory of books that are being sold at the shop. The list includes details such as author, title, price, publisher and stock position. Whenever a customer wants a book, the sales person inputs the title and the author and the system searches the list and displays whether it is available or not. If it is not, an appropriate message is displayed. If it is, then the system displays the book details and requests for the number of copies required. If the requested copies are available, the total cost is displayed; otherwise the message "insufficient Stock" is displayed. Design a system using a class called Books with suitable members.

methods declaration ;
}

The definition is very similar to a normal class definition except for the use of colon: and baseclass-name. The colon signifies that the properties of the baseclass are extended to the subclass-name. When implemented the subclass will contain its own members as well those of the baseclass. This kind of situation occurs when we want to add more properties to an existing class without actually modifying it. For example:

```csharp
class Cylinder : Circle
{
    // Add additional fields
    // and methods here
}
```

Circle is the name of an existing class containing value of the radius and Cylinder is the name of derived class which could declare the length of the cylinder as an additional data member and a method to compute its volume.

Program 13.1 illustrates the concept of simple inheritance.

## Program 13.1 ILLUSTRATION OF A SIMPLE INHERITANCE

```csharp
using System;
class Item
{
    public void Company ()        // base class
    {
        Console.WriteLine("Item Code = XXX");
    }
}

class Fan : Item                // derived class
{
    public void Model ()
    {
        Console.WriteLine("Fan Model : Classic");
    }
}

class SimpleInheritance
{
    public static void Main()
    {
        Item item = new Item();
        Fan fan = new Fan();
        item.Company();
        fan.Company();
        fan.Model();
    }
}
```
