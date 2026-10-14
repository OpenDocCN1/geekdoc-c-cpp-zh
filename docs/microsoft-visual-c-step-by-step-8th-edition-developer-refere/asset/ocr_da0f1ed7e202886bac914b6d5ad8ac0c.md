```
class Complex
{
    ...
    public static explicit operator int(Complex from)
    {
        return from.Real;
    }
    ...
}
```

This operator takes a Complex object and returns the value of the Real property. This conversion discards the imaginary element of the complex number.

4. Display the Program.cs file in the Code and Text Editor window. Add the following code shown in bold to the end of the doWork method:

Click here to view code image

```
static void doWork()
{
    ...
    Console.WriteLine($"Current value of temp is {temp}");
    if (temp == 2)
    {
        Console.WriteLine("Comparison after conversion: temp == 2");
    }
    else
    {
        Console.WriteLine("Comparison after conversion: temp != 2");
    }
    temp += 2;
    Console.WriteLine($"Value after adding 2: temp = {temp}");
}
```

These statements test the implicit operator that converts an int to a Complex object. The if statement compares a Complex object to an int. The compiler generates code that converts the int into a Complex object first and then invokes the == operator of the Complex class. The statement that adds 2 to the temp variable converts the int value 2 into a Complex object and then uses the + operator of the Complex class.

5. Add the following statements to end of the doWork method:

Click here to view code image

```
static void doWork()
{
    ...
    int tempInt = temp;
    Console.WriteLine($"Int value after conversion: tempInt == 
```