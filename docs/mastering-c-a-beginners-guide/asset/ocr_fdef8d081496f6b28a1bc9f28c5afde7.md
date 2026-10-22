Take an example, let’s see what a typical reflection flow looks like:

```
EmployeeFactory employeeFactory =
GetEmployeeFactory();
object firstEmployee = employeeFactory.
GetFirstEmployee();
Type firstEmployeeType = firstEmployee.
GetType();
object workStatusObject =
firstEmployeeType.
InvokeMember("GetWorkStatus", BindingFlags.
InvokeMethod, null, firstEmployee, null);
WorkStatus workStatus = Enum.Parse<WorkStatus>(workStatusObject.ToString());
Console.WriteLine(workStatus);
```

Although very complicated and extensive for its purpose, this piece of code retrieves an employee’s work status. All of that code was written to call a single method.

Because our EmployeeFactory class returns a generic System as an employee, this is the case. Type of object. System. The object is the basic class for all other classes, and we may use it if we don’t know what type of object we should anticipate.

To call the method of a System and for the object, we must first determine what type of object it is. We do that by calling the object.GetType() method. Then, using the InvokeMember() method, we’ll be able to execute the GetWorkStatus function on the firstEmployee object.

We can finally determine the firstEmployee’s work status after some enum parsing.

A bit complicated as it seems, but it works.