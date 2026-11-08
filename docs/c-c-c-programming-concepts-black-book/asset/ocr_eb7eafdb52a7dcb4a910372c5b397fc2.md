```
```csharp
{
    try
    {
        Console.WriteLine("Enter the first number:");
        int num1 = Convert.ToInt32(Console.ReadLine());

        Console.WriteLine("Enter the second number:");
        int num2 = Convert.ToInt32(Console.ReadLine());
        int div = num1 / num2;
        Console.WriteLine("The result of division is {0}", div);
    }
    catch (Exception ex)
    {
        Console.WriteLine("Exception occurred!!!");
        Console.WriteLine(ex.Message);
    }
}
```
```

The preceding program accepts two integers, num1 and num2. The output of the program is given as follows:

```
```text
Enter the first number:
5
Enter the second number:
0
Exception occurred!!!
Attempted to divide by zero.
```
```

We have provided the first integer as 5 and the second integer as 0. On dividing 5 by 0, the compiler would throw an exception, as 5 cannot be divided by 0. Therefore, when an exception occurs in the try block, the control of the program is transferred to the catch block.

Let's now summarize the main points discussed in the chapter.

# ## Summary

In this chapter, we have touched almost every possible aspect of LINQ. First, we have learned about LINQ and its requirement in the .NET architecture. Then, we have discussed anonymous method and lambda expression. Next, we have learned about comprehensive query, lambda query, and the deferred and immediate executions. We have also learned about LINQ to Object, LINQ to XML, and LINQ to ADO.NET. Moreover, the chapter has discussed expression tree in LINQ. Next, the filtering operators, projecting operators, joining operators, grouping operators, set operators, conversion operators, partitioning operators, equality operator, element operators, aggregation operators, and quantification operators are discussed. Finally, we have learned about exception handling using the try-catch-finally block.

# ## Quick Revise

# ### Multiple Choice Questions

+   Q1. LINQ is the abbreviation of
+       i. Linear Integrated Query
+       ii. Linear Integral Query
+       iii. Language-Integrated Query
+       iv. Language Integral Query