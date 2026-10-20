
GetArea() and Display() can also access those variables directly without the use of any instance of the class. Display(), the member function, has also been declared public. This allows it to be accessed as well from Main() with the instance r of the Rectangle class.

## Private Access Specifier

With this specifier, a class can hide the member functions and member variables from the other objects and functions. Only the functions belonging to the same class can access the private members. It is not even possible for an instance of class to access the private members.

The example given below illustrates the concept of private access specifiers.

```
using System;

namespace RectangleApplication
{

class Rectangle
{

//member variables

private double length;

private double width;
```

```
Length: 4.4
Width: 3.3
Area: 14.52
```

In the example shown above, you will have noticed that the member variables width and length have been declared private. Therefore, it is not possible to access them from the function Main(). Only the member functions Display() and AcceptDetails() can access those variables. As these member functions have been declared public, it is possible to access them from Main() with the instance r of the Rectangle Class.

## Protected Access Specifier

This specifier will enable a child class to get access to the member functions and member variables of the base class. As a result, the specifier is useful in the implementation of inheritance.

## Internal Access Specifier

This specifier will permit a class to expose its member functions and member variables to the other objects and functions in the current assembly. That is to say, a member with an internal access specifier is accessible from any method or class that has been defined within the application in which that member has been defined.

Take a look at the following example to get a better understanding of this specifier.

```
using System;

namespace RectangleApplication
{
    class Rectangle
    {
        //member variables
        internal double length;
        internal double width;
        double GetArea()
        {
            return length * width;
        }
        public void Display()
        {
            Console.WriteLine("Length: {0}", length);
            Console.WriteLine("Width: {0}", width);
            Console.WriteLine("Area: {0}", GetArea());
        }
    }//end class Rectangle

    class ExecuteRectangle
    {
        static void Main(string[] args)
        {
            Rectangle r = new Rectangle();
            r.length = 4.5;
            r.width = 3.5;
            r.Display();
            Console.ReadLine();
        }
    }
}
```

On executing the above code, the following result is achieved.

```
Length: 4.5
Width: 3.5
Area: 15.75
```

As you will notice in the example, GetArea() has not been declared with any access specifiers. If an access specifier has not been mentioned, the class member will be given the default access specifier of private.

## Protected Internal Access Specifier

This access specifier allows the class to make its member functions and member variables hidden from the other class functions and objects. Only the child classes, if any, within the same application will get access to those members. This access specifier is often used in the implementation of inheritance.

## Chapter 7: Get Introduced To Classes in C# and Their Properties

As you can recall, C# is an object oriented programming language. If you know a bit of computer programming, you will have certainly heard of classes. Classes are absolutely vital in object oriented programming.

A class can be said to be a construct with which you can build custom types by bringing together variables of different types, events and methods. A class, in other words, is a group which contains variables and methods which are related together. A class will be describing these things. In the majority of cases, you will be creating an instance of the class, which will be referred to as the object. You can use the defined variables and methods on this object. It is certainly possible to create multiple instances of the class as per the requirements of your code.

### Understanding Classes

You will have already come across the use of classes in the previous examples. After all, anything you build in C# will have to be built on classes. A better understanding can be gained by use of the following example.

```
using System;

namespace ConsoleApplication1
{
    class Program
    {
        static void Main(string[] args)
        {
            Car car;
            car = new Car("Red");
            Console.WriteLine(car.Describe());
            car = new Car("Green");
            Console.WriteLine(car.Describe());
            Console.ReadLine();
        }
    }
}

class Car
{
    private string color;
    public Car(string color)
    {
        this.color = color;
    }
    public string Describe()
    {
        return "This car is " + Color;
    }
    public string Color
    {
        get { return color; }
        set { color = value; }
    }
}
```

As you can see, a new class has been defined first and has been named as Car. To make it easier, the class has been declared alongside the main application in the same file. Generally, new classes tend to be defined in their very own files, however,

A single variable has also been defined and is called color. Moreover, it has been declared as a private variable. This is something that you should keep in mind. A property should generally be used for accessing variables from outside. At the end of the Car class, the Color property has been defined. This allows the color variable to be accessed.

A constructor has also been defined by the Car class and it is taking a parameter. This allows us to use a color to initialize the Car objects. As there is a single constructor in this application, only a color can be used for instantiating the Car objects.

The Describe() method has also been used. Its purpose is to allow the users to enjoy some extra text along with the information that has been recorded. It will only return a string along with the data that has been provided.

In the primary application, a variable has been declared, and it is of the type Car. This is followed by the creation of a new instance keeping the parameter as “Red”. As per the coding of the class, the color red is going to be allocated as the car’s color.

In order to verify that this is the case, the Describe() method is used again.

The same steps are performed once again in order to show you that it is actually quite easy to create multiple instances of the same class. Of course, another color has been used this time around.

### Understanding Properties of a Class

The job of properties is to enable you to control how accessible the variables of a class are. Properties are always the recommended way for accessing the variables from outside in any object oriented programming language. You will have already come across the use of properties in the previous example.

A property can be said to be a combination of a method and a variable. As such, it cannot take any parameters. On the other hand, the value can be processed before it is assigned to be returned. A property will consist of two sections. There will be a get method and a set method. Both of them will be taken together inside the property. You can see an example of this in the following code.

```
private string color;
public string Color
{
    get { return color; }
    set { color = value; }
}
```

The get method must be used for returning the variable. On the other hand, the set method must be used for assigning a value to that variable. Of course, the above example is a very simple example of a code involving a property. As such, it is certainly possible to extend it further.

There is another thing that you should understand about properties. A property requires at least one method to work. In other words, you can use either a get method or a set method. The other method becomes optional in these cases. This technique allows you to define read-only properties or write-only properties as per your requirements.

Here is another example that further illustrates the potential of properties.

```
public string Color
{
    get
    {
        return color.ToUpper();
    }
}
```
