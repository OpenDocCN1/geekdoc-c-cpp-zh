+   4. In the **Programs.cs** file, *add* the code snippet given in Listing 4.3:

**Listing 4.3: Passing Parameters to a Method**

```
```csharp
public static int GetSum(params int[] numbers)
{
    int sum = 0;
    foreach (int num in numbers)
        sum += num;
    return sum;
}
```
```

In Listing 4.3, a method called **GetSum()** is defined, which takes variable number of arguments. An integer variable, **sum** is declared and initialized to 0 inside the **GetSum()** method. The **foreach** loop is used to iterate over all the numbers the **GetSum()** method accepts as arguments and assign the sum of all these numbers to the variable sum. Finally, the value inside the variable sum is returned.

To call the **GetSum()** method, perform the following steps:

+   1. Call the **GetSum()** method by *adding* the highlighted code snippet given in Listing 4.4 to the **Main()** method of the **Program** class in the *PassingParameters* application:

**Listing 4.4: Calling a Parameterized Method**

```
```csharp
static void Main(string[] args)
{
    Console.WriteLine("The sum is:");
    Console.WriteLine(GetSum(1, 2, 3, 4, 5, 6, 7, 8, 9));
    Console.WriteLine(GetSum(2, 4, 6, 8));
    Console.WriteLine("\nPress ENTER to quit...");
    Console.ReadLine();
}
```
```

In Listing 4.4, the **GetSum()** method is first called by passing nine numbers as arguments and then called again by passing four numbers as arguments.

+   2. Press the **F5** key to run the *PassingParameters* application.

The output of the application appears, as shown in Fig.C#-4.3.

![](bbox=[0.341, 0.614, 0.612, 0.684])

**Fig.C#-4.3**

In Fig.C#-4.3, you can see that when the **GetSum()** method is called first, it returns the sum of all the nine numbers; when the **GetSum()** method is called by passing four numbers as arguments, it returns the sum of all the four numbers.

Now that you know how to pass parameters to a method, let's discuss the ways in which you can pass parameters to a method. C# allows methods to be passed either by value or by reference. Let's first discuss how to pass a parameter by value in the following section.

# ## Pass by Value

When a parameter is passed by value, a copy of the variable is passed into the method being called. The changes to the parameter that take place inside the method body do not affect the original data. Let's perform the following steps to pass a parameter by value:

+   1. *Repeat* steps 1 to 3 of the **Defining a Method** section of this chapter.