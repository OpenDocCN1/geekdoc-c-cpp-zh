selectedEmployee, and I point that variable to one of the employees already in the list.

```
Console.WriteLine("Creating an employee");
Console.Write("Enter the first name: ");
string firstName = Console.ReadLine();

Console.Write("Enter the last name: ");
string lastName = Console.ReadLine();

Console.Write("Enter the hourly rate: ");
string hourlyRate = Console.ReadLine();
double rate = double.Parse(hourlyRate);//we will assume here that input is in the correct format
```

And it's based on the selection made by the user. On that selectedEmployee, we then call the PerformWork, and that will point to an object that is actually our selectedEmployee object, and we call the PerformWork method on that. That now accepted the hours worked, and therefore, I'll pass here that number of hours as a variable. This variation is also returning the number of hours worked, so I can capture that here in the local variable, numberOfHoursWorked. That is a local variable here, and then used' in that output. The PayEmployee method is pretty similar. This part is, well, pretty much the same. The only thing that is really different is the out parameter that you see here. I don't initialize the hours worked, but I do pass it in as an out parameter. When I call the ReceiveWage method on the selectedEmployee, I then get back that value as a double, but I also get a value for hours worked, and it is then used here in the output. You now should have a good understanding of classes and objects, and so now would be a good time to build something on your own. I suggest you do an exercise at this point. Given the application we just looked at, try extending it. First, extend the application so that it's possible to change the hourly rate we passed in initially using the constructor for a selected employee. Secondly, add the option to assign a bonus for an