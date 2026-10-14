18. Add the statements that follow (shown in bold) to the doWork method after the code you just wrote. These statements create an instance of the Car class and test its methods.

Click here to view code image

```
static void doWork()
{
    ...
    Console.WriteLine("\nJourney by car:");
    Car myCar = new Car();
    myCar.StartEngine("Brm brm");
    myCar.Accelerate();
    myCar.Drive();
    myCar.Brake();
    myCar.StopEngine("Phut phut");
}
```

19. On the Debug menu, click Start Without Debugging.
In the console window, verify that the program outputs messages simulating the different stages of performing a journey by airplane and by car, as shown in the following image:

![](bbox=[0.3, 0.47, 0.7, 0.65])

Notice that both modes of transport invoke the default implementation of the virtual Drive method because neither class currently overrides this method.

20. Press Enter to close the application and return to Visual Studio 2015.

21. Display the Airplane class in the Code and Text Editor window. Override the Drive method in the Airplane class, as follows in bold:

Click here to view code image

```
class Airplane : Vehicle
{
    ...
    public override void Drive()
    {
        Console.WriteLine("Flying");
    }
}
```