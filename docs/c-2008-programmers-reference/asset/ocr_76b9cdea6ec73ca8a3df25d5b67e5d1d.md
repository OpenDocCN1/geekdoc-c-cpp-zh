# Rethrowing Exceptions

There are times when after catching an exception, you want to throw the same (or a new type) exception back to the calling function after taking some corrective actions. Take a look at this example:

```
```csharp
class Program
{
    static void Main(string[] args)
    {
        int num1, num2, result;
        try
        {
            Console.Write("Please enter the first number:");
            num1 = int.Parse(Console.ReadLine());

            Console.Write("Please enter the second number:");
            num2 = int.Parse(Console.ReadLine());

            Program myApp = new Program();

            Console.WriteLine("The result of {0}/({1} is {2}",
                num1, num2,
                myApp.PerformDivision(num1, num2));
        }
        catch (Exception ex)
        {
            Console.WriteLine(ex.Message);
            if (ex.InnerException != null)
                Console.WriteLine(ex.InnerException.ToString());
        }
        Console.ReadLine();
    }

    private int PerformDivision(int num1, int num2)
    {
        try
        {
            return num1 / num2;
        }
        catch (DivideByZeroException ex)
        {
            throw new Exception("Division by zero error.", ex);
        }
    }
}
```
```

Here, the PerformDivision() function tries to catch the DivideByZeroException exception and once it succeeds, it rethrows a new generic Exception exception, using the following statements with two arguments:

```
```csharp
throw new Exception("Division by zero error.", ex);
```
```