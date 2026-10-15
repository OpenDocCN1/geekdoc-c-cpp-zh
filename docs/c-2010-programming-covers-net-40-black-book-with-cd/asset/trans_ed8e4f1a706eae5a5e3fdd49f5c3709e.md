

new Console application, named MyCopyConstructor (also available in the CD) by performing the steps given in the section, Creating a Namespace. Then replace the default code of the Program.cs file of the application with the code shown in Listing 4.15:

## Listing 4.15: Showing the Code of the MyCopyConstructor Application

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

namespace MyCopyConstructor
{
    class Program
    {
        static void Main(string[] args)
        {
            // Create a new CarDetails object.
            CarDetails car1 = new CarDetails("Zen Estilo VXI", 15.7);

            // Create another new object, copying car1.
            CarDetails car2 = new CarDetails(car1);
            Console.WriteLine(car2.Details);
            Console.Write("\nPress ENTER to Quit..");
            Console.ReadLine();
        }
    }
    class CarDetails
    {
        private string ModelName;
        private double Mileage;
        // Copy constructor.
        public CarDetails(CarDetails MyCar)
        {
            ModelName = MyCar.ModelName;
            Mileage = MyCar.Mileage;
        }
        // Instance constructor.
        public CarDetails(string ModelName, double Mileage)
        {
            this.ModelName = ModelName;
            this.Mileage = Mileage;
        }
        public string Details
        {
            get
            {
                return ("Car " + ModelName + " has the Average of " + Mileage + "km/lit");
            }
        }
    }
```

In Listing 4.15, we first create an object of the CarDetails class, car1, by passing two arguments to the constructor of the CarDetails class. Then, we create another object of the CarDetails class, car2, by copying the data of the car1 object.

Figure 4.17 shows the output of the MyCopyConstructor application:

![](img/e073a4882197be4ab61103cbe0bcb394_211_0.png)

## Figure 4.17: Showing the MyCopyConstructor Application

## Calling the Destructor of a Class

Destructor is a method that is called to destroy the objects that are no longer in use. A class can have only one destructor. A destructor is declared using the tilde (~) sign, followed by the name of the destructor. To see how to create a destructor of a class, first create a new Console application, named MyDestructor (also available in the CD) and then replace the default code of the Program.cs file of the application with the code shown in Listing 4.16:

## Listing 4.16: Showing the Code of the MyDestructor Application

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
namespace MyDestructor
{
    class Program
    {
        static void Main(string[] args)
        {
            Destruct obj = new Destruct();
        }
    }
    class Destruct
    {
        ~Destruct()
        {
            Console.WriteLine("Destructor is Called");
            Console.Write("\nPress ENTER to Quit..");
            Console.ReadLine();
        }
    }
}
```

In Listing 4.16, a destructor, Destruct, is called automatically. This destructor destroys the obj object of the Destruct class, when it is no longer in use. Figure 4.18 shows the output of the MyDestructor application:

![](img/e073a4882197be4ab61103cbe0bcb394_212_0.png)

Figure 4.18: Showing the Output of the MyDestructor Application

The message Destructor is Called appears on the screen for a moment (Figure 4.18) and then the application terminates.

## Creating a Static Class

You already learned about the static class in the In Depth section of this chapter. You can declare a static class by the static keyword. When a class is declared static, there is no need to create the objects of the class because the members of a static class can be accessed by the class name rather than the object of the class.

Listing 4.17 shows how to create a static class:

## Listing 4.17: Showing the Code to Create a Static Class

```
public static class TemperatureConverter
{
    public static double CelsiusToFahrenheit(string temperatureCelsius)
    {
        //Method body

```

In Listing 4.17, we create a static class, TemperatureConverter, with two static methods CelsiusToFahrenheit() and FahrenheitToCelsius().

## Using a Static Method in Classes

You can call a static method with a class name even without creating the instance of the class. If you create an instance of the class, then you cannot use it to access static members. A static member can exist inside a static class or a non-static class. To see how to define static methods in a class, first create a new Console application named MyStaticMethod (also available in the CD) and then replace the default code of the Program.cs file of the application with the code shown in Listing 4.18:

Listing 4.18: Showing the Code of the MyStaticMethod Application

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
namespace MyStaticMethod
{
    class Program
    {
        static void Main(string[] args)
        {
            Console.WriteLine("Please Select The Convertor");
            Console.WriteLine("1. Celsius to Fahrenheit");
            Console.WriteLine("2. Fahrenheit to Celsius");
            Console.Write("\nPress either 1 or 2:");
            string Selection;
            Selection = Console.ReadLine();
            double F, C = 0;
            switch (Selection)
            {
                case "1":
                    Console.Write("Please enter the Celsius temperature: ");
                    F = TemperatureConverter.CelsiusToFahrenheit(System.Console.ReadLine());
                    Console.WriteLine("Temperature in Fahrenheit: {0:F2}", F);
                    break;
                case "2":
                    Console.Write("Please enter the Fahrenheit temperature: ");
                    C = TemperatureConverter.FahrenheitToCelsius(System.Console.ReadLine());
                    Console.WriteLine("Temperature in Celsius: {0:F2}", C);
                    break;
                default:
                    Console.WriteLine("Please select a convertor.");
                    break;
            }
            Console.Write("\nPress ENTER to Quit..");
            Console.ReadLine();
        }
    }
    public static class TemperatureConverter
    {
        public static double CelsiusToFahrenheit(string temperatureCelsius)
        {
            // Convert argument to double for calculations.
            double celsius = Double.Parse(temperatureCelsius);
            // Convert celsius to Fahrenheit.
            double fahrenheit = (celsius * 9 / 5) + 32;

```

```
public static double FahrenheitToCelsius(string temperatureFahrenheit)
{
    //Method body
}
```

```
return fahrenheit;
}
public static double FahrenheitToCelsius(string temperatureFahrenheit)
{
    // Convert argument to double for calculations.
    double fahrenheit = Double.Parse(temperatureFahrenheit);
    // Convert Fahrenheit to Celsius.
    double celsius = (fahrenheit - 32) * 5 / 9;
    return celsius;
}
}
```

In Listing 4.18, two static methods, CelsiusToFahrenheit() and FahrenheitToCelsius(), are declared inside a static class, TemperatureConverter. No instance of the TemperatureConverter class is created and the methods inside the class are accessed by the class name.

Now, press the F5 key to run the MyStaticMethod example. The user is prompted to select the convertor. To select the Celsius to Fahrenheit converter, press 1 and to select the Fahrenheit to Celsius convertor, press 2. In this case, we have pressed 1. Now, enter the Celsius temperature, say 40, and press the Enter key. You get the temperature in Fahrenheit, as shown in Figure 4.19:

![](img/e073a4882197be4ab61103cbe0bcb394_214_0.png)

## Assigning and Retrieving Values Using a Property

Properties allow you to access the internal data of a class in a less cumbersome manner. Earlier, programmers were required to define two separate methods—one for assigning a value to a variable and the other for retrieving the value of a variable. When you create a property, the compiler automatically generates class methods to set and get the property value and makes calls to these methods automatically when a programmer uses the property. To see how to assign and retrieve values using a property, first create a new Console application, named MyProperty (also available in the CD) and then replace the default code of the Program.cs file of the application with the code given in Listing 4.19:

Listing 4.19: Showing the Code of the MyProperty Application

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

namespace MyProperty
{
    class Person
    {
        private string MyName = "";
        private int MyAge = 0;
        // Declare a Name property of type string:
        public string Name
        {
            get
            {
                return MyName;
```
