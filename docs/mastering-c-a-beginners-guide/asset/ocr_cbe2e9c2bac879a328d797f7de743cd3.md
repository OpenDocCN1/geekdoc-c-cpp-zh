```
public static void Main(string[] args)
{
    Car objCar = new Car();
    Console.WriteLine("Car mileage is : " + objCar.GetMileage()); // accessible outside "Car"

    Console.WriteLine("Car color is : " + objCar.GetColor()); //accessible outside "Car"
    //we can’t call this method as it is inaccessible outside "Car"
    //objCar.GetEngineMakeFormula(); //commented because we can’t access it
    Console.WriteLine("Car color is : " + objCar.DisplayMakeFormula()); // accessible outside
    Console.Read();
}
```

As you can see from the above code that necessary methods and properties are exposed using public access modifier, and unnecessary methods and properties are hidden using private access modifier. This way, we can implement abstraction, or we can achieve abstraction in our code or web application.

# Inheritance

The inheritance is a way to make new classes using classes that have already been defined. The newly formed classes