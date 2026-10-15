```
class Program
{
    static void Main(string[] args)
    {
        Console.WriteLine("Creating a lot of employees!");
        Console.WriteLine("--------------------------\n");
        List<Employee> employees = new List<Employee>();
        for (int i = 0; i < 1000000; i++)
        {
            Employee randomEmployee = new Employee(Guid.NewGuid().ToString(), Guid.NewGuid().ToString(),
                Guid.NewGuid().ToString(), new DateTime(1979, 1, 16), EmployeeType.StoreManager, null);
            employees.Add(randomEmployee);
        }
        employees.Clear();
        employees = null;
        Console.ReadLine();
    }
}
```

Even if you invoke it, it's not guaranteed to run. It is determined by the CLR if it will run at that time or not based on several parameters, such as load on the system. In the final demonstration of this chapter, let's take a look at garbage collection. Though it's a process you typically don't see, I'm going to show you a few things in this area. For the sake of this demonstration, I have removed a lot of the code that we had already in the Program class, and I have replaced it with what you see here. I'm now going to create a large number of employees to try show you how C# or .NET behaves in combination with garbage collection. I'm creating a list of employees. The list type is a type, we've touched on it already before, it comes with C#. Try to bring in the system collections generic using statement at the top, and it's used to store a list of objects. In the for loop, I'm going to create a large number of employees and I'm going to add them to that list. Below that, I'm going to clear the list and I'm going to set the employees back to null. Let's now run this application and see how this behaves. W doing this I'm going to open the Diagnostic Tools in Visual Studio. You can find them under