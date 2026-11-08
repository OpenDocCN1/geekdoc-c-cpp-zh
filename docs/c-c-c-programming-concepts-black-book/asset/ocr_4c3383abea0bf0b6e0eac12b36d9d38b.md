The preceding program is the modification of Listing 17.52. In this program, we have changed the values of the item1 and item2 variables by using the ref keyword and then printed the values.

The output of the program is given as follows:

```
```
The addition is: 50
The value of item1 is: 20
The value of item2 is: 30
```
```

# Passing a Reference using the out Keyword

Unlike reference parameter, the out parameter is unidirectional and it only returns the changed values from the method that has been called. Listing 17.54 shows an example of the out keyword:

Listing 17.54: Showing an Example of Passing Reference using the out Keyword

```
```csharp
using System;
class Program
{
    public static void Main()
    {
        int item1 = 10;
        int item2= 10;
        int item3 = 0;
        int item4 = 0;
        Addition addition = new Addition();
        //Passing reference with "out" keyword to the method Add()
        int result = addition.Add(item1, item2, out item3, out item4);
        Console.WriteLine("The addition is: {0}", result);
        Console.WriteLine("The value of item1 is: {0}",item1);
        Console.WriteLine("The value of item2 is: {0}", item2);
        Console.WriteLine("The value of item3 is: {0}", item3);
        Console.WriteLine("The value of item4 is: {0}", item4);
    }
}
class Addition
{
    public Addition()
    {
    }
    public int Add(int item1,int item2, out int item3, out int item4)
    {
        item3 = item1 + 10;
        item4 = item2 + 20;
        return (item3 + item4);
    }
}
```
```

The code in the preceding program is the modification of Listing 17.52. In this program, we are passing the values and in turn getting the processed values of the item1 and item2 variables as item3 and item4 respectively whose type is set to out.

The output of the program is given as follows:

```
```
The addition is: 50
The value of item1 is: 10
The value of item2 is: 10
The value of item3 is: 20
The value of item4 is: 30
```
```