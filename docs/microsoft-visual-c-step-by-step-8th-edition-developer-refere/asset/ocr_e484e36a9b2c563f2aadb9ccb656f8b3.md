# Note

IntelliSense displays a list of available virtual methods. If you select the Drive method from the IntelliSense list, Visual Studio automatically inserts into your code a statement that calls the base.Drive method. If this happens, delete the statement, because this exercise does not require it.

22. Display the Car class in the Code and Text Editor window. Override the Drive method in the Car class, as shown in bold in the following:

Click here to view code image

```
class Car : Vehicle
{
    ...
    public override void Drive()
    {
        Console.WriteLine("Motoring");
    }
}
```

23. On the Debug menu, click Start Without Debugging.

In the console window, notice that the Airplane object now displays the message Flying when the application calls the Drive method, and the Car object displays the message Motoring:

![](bbox=[0.182, 0.534, 0.825, 0.875])

24. Press Enter to close the application and return to Visual Studio 2015.

25. Display the Program.cs file in the Code and Text Editor window.