# 21.9 Lambda Expressions 905

```
// Fig. 21.7: Lambdas.cs
// Using lambda expressions.
using System;
using System.Collections.Generic;

class Lambdas{
    // delegate for a function that receives an int and returns a bool
    public delegate bool NumberPredicate(int number);

    static void Main(string[] args)
{
        int[] numbers = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10};

        // create an instance of the NumberPredicate delegate using an
        // implicit lambda expression
        NumberPredicate evenPredicate = number => number % 2 == 0;

        // call a lambda expression through a variable
        Console.WriteLine($"Use a lambda-expression variable: {evenPredicate(4)}");

        List<int> evenNumbers = FilterArray(numbers, evenPredicate);

        // display the result
        DisplayList("Use a lambda expression to filter even numbers: ", evenNumbers);

        // filter the odd numbers using an explicitly typed lambda
        List<int> oddNumbers = FilterArray(numbers, int number) => number % 2 == 1);

        // display the result
        DisplayList("Use a lambda expression to filter odd numbers: ", oddNumbers);

        // filter numbers greater than 5 using an implicit lambda statement
        List<int> over5 = FilterArray(numbers, number => {return number > 5});

        // display the result
        DisplayList("Use a lambda expression to filter numbers over 5: ", over5);
    }

    // select an array's elements that satisfy the predicate
    private static List<int> FilterArray(
        int[] array, NumberPredicate predicate)
    {
        // hold the selected elements
        var result = new List<int>();
    }
```

Fig. 21.7 | Using lambda expressions. (Part I of 2.)