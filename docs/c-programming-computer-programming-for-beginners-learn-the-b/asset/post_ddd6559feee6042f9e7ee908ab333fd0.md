
}
set
{
    if (value == "Red")
        color = value;
    else
        Console.WriteLine("This car can only be red!");
}
As you can see, this a more complex piece of code featuring a more advanced property. Now, you will find that the color variable is going to be returned in only uppercase characters. This is due to the addition of the ToUpper() method to the variable before it is returned. The next section of the code will set the color variable. However, the only value that will be accepted is “Red”.

## A Short Guide to Visibility

Throughout this guide, you will have come across the terms public and private. You may have been wondering as to what they stand for. Well, they are keywords that denote the visibility of the item in question.

the class of the protected internal item can access that item even if the inherited classes are present in another project.

You should now be able to create simple classes on your own and even create their properties. Of course, this is only the basic level. With practice and further knowledge, you can create incredibly complex and awesome programs featuring multiple classes and properties.

## Getting a Grip on Member Functions and Encapsulation

In class, a member function is a function which has its prototype or definition within the class definition in a similar manner to other variables. A member function can operate on any object of its class. It also has access to each and every member of the class for that object.

On the other hand, member variables are attributes for an object. As such, they will be kept private in order to implement encapsulation. They can only be accessed by use of the public member functions.

The following example illustrates the use of class members. Here, the value of the different class members is being sought.

```
using System;
```
```
namespace BoxApplication
```
```
{
```
```
class Box
{
    private double length; // Length of a box
    private double breadth; // Breadth of a box
    private double height; // Height of a box
    public void setLength( double len )
    {
        length = len;
    }
    public void setBreadth( double bre )
    {
        breadth = bre;
    }
    public void setHeight( double hei )
    {
        height = hei;
    }
    public double getVolume()
```
```
Box2.setBreadth(13.0);
Box2.setHeight(10.0);
// volume of box 1
volume = Box1.getVolume();
Console.WriteLine("Volume of Box1 :{0}",volume);
// volume of box 2
volume = Box2.getVolume();
Console.WriteLine("Volume of Box2 :{0}",volume);
Console.ReadKey();
}
}
}
```

On executing the code given above, the following result will be produced.

Volume of Box1 :210

Volume of Box2 :1560

## Static Members of a Class in C#

Class members can be defined as static with the help of the static keyword. On declaring a specific member of the class as static,

there will only be a single copy of that static member irrespective of the number of objects created for that class.

In other words, the static keyword denotes that only a single instance of that member will exist for a class. Static variables tend to be used in defining constants. This is due to the fact that it is possible to retrieve their values by invoking the class without the creation of an instance. The initialization of static variables can take place outside the class definition or member function. At the same time, static variables can be initialized inside the class definition.

Take a look at the following example.

```
using System;

namespace StaticVarApplication
{
    class StaticVar
    {
        public static int num;
        public void count()
        {
            num++;
```
```
}

public int getNum()
{
    return num;
}

}

class StaticTester
{
    static void Main(string[] args)
    {
        StaticVar s1 = new StaticVar();
        StaticVar s2 = new StaticVar();

        s1.count();
        s1.count();
        s1.count();

        s2.count();
        s2.count();
        s2.count();
    }
}
```
```
```
```
Console.WriteLine("Variable num for s1: {0}",
s1.getNum());
Console.WriteLine("Variable num for s2: {0}",
s2.getNum());
Console.ReadKey();
}
}
}
```
```

The following result is produced when you execute the code shown above.

Variable num for s1: 6

Variable num for s2: 6

A member function can also be declared as static. These functions will be accessed static variables only. Moreover, static functions can exist even before the creation of the object.

Take a look at the following example to get a better understanding of these static functions.

```
```csharp
using System;
namespace StaticVarApplication
{
```
```
class StaticVar
{
public static int num;
public void count()
{
num++;
}
public static int getNum()
{
return num;
}
}

class StaticTester
{
static void Main(String[] args)
{
StaticVar s = new StaticVar();
s.count();
}
}
```
```
s.count();

s.count();

Console.WriteLine("Variable    num:    {0}", StaticVar.getNum());

Console.ReadKey();
}
}
}
```

On compiling and executing the above code, you will find the following result to be produced.

Variable num: 3

## Chapter 8

## A Brief on Methods

As you have been reading this book, you will have come across methods more than once. If you were wondering what they are, well, this is where you get to know about them. Methods are one of the basic things about programming that you should know about.

## What is a Method?

A method can be said to be a group of statements that can perform a task together. All programs in C# will have one class at the very least that contains a method with the name of Main. You will have already come across them.

In order to use a method, the method will have to be defined first. Then, the method will be called. Let’s take a look at each of this process.

## Defining a Method

When a method is defined, the elements of the method’s structure are declared. The syntax for defining a method in the C# language is given as shown.

```
<Access Specifier> <Return Type> <Method Name>(Parameter List)
```
```
{
```
```
Method Body
```
```
}
```

A method can have various elements. They are mentioned as follows.

Access Specifier: As you already know, the access specifier will determine the visibility of a method or a variable from another class.

Return Type: It is possible for methods to return values. The return type states the datatype of the value that will be returned by the method. If there are no values being returned by the method, then the return type will be void.

Method name: This is the unique identifier of the method name. The name is case sensitive. Moreover, the identifier cannot be the same as any of the other identifiers that have been declared in the class.

Parameter list: The parameters are what are used for passing and receiving data from methods. They are enclosed in parentheses. The parameter list will refer to the order, number and type of parameters of the method. Importantly, it is possible for a method not to have any parameters.

Method Body: The body will contain the set of instructions that is necessary for the completion of the activity.

Take a look at the example given below. In this snippet of code, you will notice a function FindMax. It takes two integer values and compares them. The larger of the values will be returned. The function has a public access specifier. Therefore, it is accessible from the outside of the class by using an instance of it.

```
class NumberManipulator
{
    public int FindMax(int num1, int num2)
    {
        /* local variable declaration */
        int result;
        if (num1 > num2)
            result = num1;
        else
```
```
result = num2;

return result;
}
...
}
```

## Calling a Method

In C#, it is quite easy to call a method as it can be done just by using its name. Take a look at the example given below. It shows how a method is called.

```
using System;

namespace CalculatorApplication
{

class NumberManipulator
{

public int FindMax(int num1, int num2)
{

/* local variable declaration */

int result;

if (num1 > num2)
```
