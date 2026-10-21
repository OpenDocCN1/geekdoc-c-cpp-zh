Program 13.8 shows the concept of polymorphism while applying multilevel inheritance. A single method is called several times in the Base class and its nested classes and different output is shown for the same method based on the calling class.

# Program 13.8 | POLYMORPHISM ILLUSTRATED FURTHER

```
using System;
using System.Collections.Generic;
using System.Text;
namespace PolymorphismExample
{
    class PolymorphismDemo
    {
        static void Main(string[] args)
        {
            Automobile a = new Automobile();
            a.PowerSource = "100 H.P.";
            a.IncreaseVelocity(60);
            BMW car = new BMW();
            car.Color("Black");
            Console.WriteLine("\nPress Enter to exit...");
            Console.ReadLine();
        }
    }
    class Vehicle
    {
        string Vehiclepower = "";
        public string PowerSource
        {
            set
            {
                Vehiclepower = value;
                Console.WriteLine("Power of engine is set to \"{0}\"", value.ToString());
            }
            get
            {
                return Vehiclepower;
            }
        }//end property PowerSource
        public virtual void IncreaseVelocity(int i)
        {
            Console.WriteLine("The speed increases to " + i.ToString() + " m.p.h.");
        } //end method IncreaseVelocity
    } //end base class Vehicle
    class Automobile : Vehicle
    {
        public override void IncreaseVelocity(int i)
        {
```