
## 12.17 THE THIS REFERENCE

C# supports the keyword this which is a reference to the object that called the method. The this reference is available within all the member methods and always refers to the current instance. It is normally used to distinguish between local and instance variables that have the same name. Consider the code segment shown below:

```
class Integers
{
    int x;
    int y;
    public void SetXY(int x, int y)
    {
        this.x = x;
        this.y = y;
    }
    ...
    ...
}
```

In the assignment statements, this.x and this.y refer to the class members named x and y whereas simple x and y refer to the parameters of the SetXY() method.

## 12.18 NESTING OF CLASSES

In C#, it is possible to define a type within the scope of another type. C# allows classes, structs, interfaces and enums to nest others. Example:

```
public class Outer
{
    ...          //Members of Outer class
    ...
    ...
    public class Inner
    {
        ...          //Members of Inner class
        ...
    }
}
```

A class can nest not only complete classes but also objects of other classes. For example:

```
public class Room
{
    ...
    ...
}
//A house has a room
public class House
{
    ...
    ...
    //The contained room
```

private Room room1;

The House class had declared the Room object room1 as one of its members. This relationship between House and Room is termed as ‘has-a’ relationship. (See Chapter 13)

Program 12.4 demonstrates the concept of nested classes and the way the methods of the Main class and the inner classes are called and displayed.

### Program 12.4 ILLUSTRATION OF NESTED CLASSES

```
using System;
using System.Collections.Generic;
using System.Text;
namespace InnerClassExample
{
    public class nestedClass
    {
        public static void Main()
        {
            outerClass obj2 = new outerClass();
            obj2.show();
            outerClass.innerClass obj1 = new outerClass.innerClass();
            obj1.display();
        }
    }
    public class outerClass
    {
        public void show()
        {
            System.Console.WriteLine("This message is from the class outerClass containing the\nnested class innerClass.\n");
        }
        public innerClass abc()
        {
            return new innerClass();
        }
        public class innerClass
        {
            public void display(){
                System.Console.WriteLine("This is a nested class example in C#.\n This info is in the innermost class innerClass.");
            }
        }
    }
}
```

## 12.19 CONSTANT MEMBERS

C# permits declaration of data fields of a class as constants. This can be done using the modifier const. Example:

```
public const int size = 100;
```

The member size is assigned the value 100 at compile time and cannot be changed later. Any attempt to assign a value to it will result in compilation error. It also means its value must be set when it is defined. For instance:

```
public const int size;
```

is wrong and will cause a compilation error. The const members are implicitly static. The value is by definition constant and therefore only one copy of it is stored which is common for all objects of the class. This implies that we must access the const members using the class name as we do with the static members.

Although const members are implicitly static, we cannot declare them so explicitly using static. For example, the statement

```
public static const int size = 100;
```

is wrong and will produce compile-time error.

## 12.20 READONLY MEMBERS

There are situations where we would like to decide the value of a constant member at run-time. We may also like to have different constant values for different objects of the class. To overcome these shortcomings, C# provides another modifier known as readonly to be used with data members. This modifier is designed to set the value of the member using a constructor method, but cannot be modified later. The readonly members may be declared as either static fields or instance fields. When they are declared as instance fields, they can take different values with different objects. Consider the code below:

```
class Numbers
{
    public readonly int m;
    public static readonly int n;
    public Numbers ( int x )
    {
        m = x;
    }
    static Numbers ()
    {
        n = 100;
    }
}
```

The value for m is provided at the time of creation of an object using the constructor with parameter x. This value will remain constant for that object. Remember, the variable n is assigned a value of 100, even before the creation of any objects of Numbers.

## 12.21 PROPERTIES

One of the design goals of object-oriented systems is not to permit any direct access to data members, because of the implications of integrity. It is normal practice to provide special methods known as accessor methods to have access to data members. We must use only these methods to set or retrieve the values of these members. Recall that we have used a method GetData() in Program 12.1 to provide values to the data members length and breadth of Rectangle class. Similarly, we could use another method to read the values of these members. Program 12.5 shows how accessor methods can be used to set and get the value of a private data member.

### Program 12.5 ACCESSING PRIVATE DATA USING ACCESSOR METHODS

```
using System;
class Number
{
    private int number;
    public void SetNumber( int x )        // accessor method
    {
        number = x;                       // private number accessible
    }
    public int GetNumber()                // accessor method
    {
        return number;
    }
}

class NumberTest
{
    public static void Main ()
    {
        Number n = new Number ();
        n.SetNumber (100);    // set value
```

```
Console.WriteLine("Number = " + n.GetNumber()); // get value
// n.number; //Error! Cannot access private data
}
```

Output of Program 12.5:
    Number = 100

The SetNumbers method is also known as the mutator method. Using accessor methods works well and is a technique used by several OOP languages, including C++ and Java. However, it suffers from the following drawbacks:

- We have to code the accessor methods manually.
- Users have to remember that they have to use accessor methods to work with data members.

In order to overcome these problems, C# provides a mechanism known as properties that has the same capabilities as accessor methods, but is much more elegant and simple to use. Using a property, a programmer can get access to data members as though they are public fields. (Properties are sometimes referred to as ‘smart fields’ as they add smartness to data fields.)

We could rewrite the code in Program 12.5 using a property as shown in Program 12.6.

### Program 12.6 IMPLEMENTING A PROPERTY

```
using System;
class Number
{
    private int number;
    public int Anumber // property
    {
        get
        {
            return number;
        }
        set
        {
            number = value;
        }
    }
}
class PropertyTest
{
    public void static Main ()
    {
        Number n = new Number ();
        n.Anumber = 100;
        int m = n.Anumber;
        Console.WriteLine("Number = " + m);
    }
}
```

The class now declares a property called A number of type int and defines a get accessor method (also known as getter) and a set accessor method (also known as setter). The getter method used the keyword return to return the field’s value to the caller. The setter method uses the keyword value to receive the value being passed in from the user. The type of value is determined by the type of property.

As the names imply, getter method is used to get (or read) the value and the setter method is used to set (or write) the value. In Program 12.6, the statement
n.Anumber = 100;
invokes the setter method and places an integer value 100 in a variable named value which in turn is assigned to the field number.

Similarly, the statement
int m = n.Anumber;
invokes the getter method and assigns the value of the property to m.

A property can omit either a get clause or the set clause. A property that has only a getter is called a read-only property, and a property that has only a setter is called a write-only property. A write-only property is very rarely used. There are other powerful features of properties. They include:

- Other than fetching the value of a variable, a get clause uses code to calculate the value of the property using other fields and returns the results. This means that properties are not simply tied to data members and they can also represent dynamic data.
- Like methods, properties are inheritable. We can use the modifiers abstract, virtual, new and override with them appropriately, so that the derived classes can implement their own versions of properties.
- The static modifier can be used to declare properties that belong to the whole class rather than to a specific instance of the class. (Like static methods, static properties cannot be declared with the virtual, abstract or override modifiers.)

An important point to note here is that we can specify any modifier only at the property level and this will affect both the accessors equally. For instance, we cannot override only one, leaving the other unaffected.

## 12.22 INDEXERS

Indexers are location indicators and are used to access class objects, just like accessing elements in an array. They are useful in cases where a class is a container for other objects.

An indexer looks like a property and is written the same way a property is written, but with two differences:

- The indexer takes an index argument and looks like an array.
- The indexer is declared using the name this.

The indexer is implemented through get and set accessors for the [ ] operator. Example:

```
public double this[ int idx ]
{
    get
    {
        //Return desired data
    }
    set
    {
```
