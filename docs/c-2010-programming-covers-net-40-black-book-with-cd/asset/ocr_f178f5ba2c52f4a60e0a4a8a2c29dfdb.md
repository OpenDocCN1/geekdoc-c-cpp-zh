```
}
set
{
    MyName = value;
}
}
// Declare an Age property of type int:
public int Age
{
    get
    {
        return MyAge;
    }
    set
    {
        MyAge = value;
    }
}
public override string ToString()
{
    return ("Name = " + Name + ", Age = " + Age);
}
public static void Main()
{
    Console.WriteLine("Simple Properties");
    // Create a new Person object:
    Person person = new Person();
    // Print out the name and the age associated with the person:
    Console.WriteLine("Person details: " + person);
    // Set some values on the person object:
    person.Name = "Umar";
    person.Age = 24;
    Console.WriteLine("Person details: " + person);
    // Increment the Age property:
    person.Age += 1;
    Console.WriteLine("Person details: " + person);
    Console.Write("\nPress ENTER to Quit..");
    Console.ReadLine();
}
}
```

Figure 4.20 shows the output of the MyProperty application:

![](bbox=[0.275, 0.62, 0.76, 0.735])

Figure 4.20: Showing the Output of the MyProperty Application

As you can see from this example, properties allow you to safely, yet conveniently, set data in a class, while retaining complete control over the validation of the data.

# Using Object Initializers

C# allows you to assign values to any accessible fields or properties of an object at the time of object creation, using the new object initializer syntax. To see how to create and initialize objects using the new object initializer syntax, first create a new Console application, named MyObjectInitializer (also available in the CD) and then replace the default code of the Program.cs file of the application with the code shown in Listing 4.20: