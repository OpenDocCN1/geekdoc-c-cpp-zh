
# 21.9 Lambda Expressions

```c
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
        List<int> oddNumbers = FilterArray(numbers, (int number) => number % 2 == 1);

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
        // iterate over each element in the array
        foreach (var item in array)
        {
            // if the element satisfies the predicate
            if (predicate(item))
            {
                result.Add(item); // add the element to the result
            }
        }
        return result; // return the result
    }

    // display the elements of a List
    static void DisplayList(string description, List<int> list)
    {
        Console.WriteLine(description); // display the output's description
        // iterate over each element in the List
        foreach (int item in list)
        {
            Console.Write($"{item}"); // print item followed by a
        }
        Console.WriteLine(); // add a new line
    }
}
```

Use a lambda-expression variable: True
Use a lambda expression to filter even numbers: 2 4 8 10
Use a lambda expression to filter odd numbers: 1 3 5 7 9
Use a lambda expression to filter numbers over 5: 6 7 8 9 10

**Fig. 21.7** Using lambda expressions. (Part 2 of 2)

## Chapter 21 Generic Collections: Functional Programming with LINQ/PLINQ

### 21.9.1 Expression Lambdas

A lambda expression (line 17)

```c
number => number % 2 == 0
```

begins with a parameter list (number in this case). The parameter list is followed by the => lambda operator (read "goes to") and an expression that represents the lambda's body. The lambda expression in line 17 uses the % operator to determine whether the parameter's value is an even int. The value produced by the expression—true if the int is, false otherwise—is implicitly returned by the lambda expression. The lambda in line 17 is called an expression lambda, because it has a single expression to the right of the lambda operator. We do not specify a type for the lambda expression—the return type is inferred from the return value or from a delegate's return type. The lambda expression in line 17 is equivalent to the IsEven method in Fig. 21.6. Note that C# 6's expression-bodied methods use a similar syntax to expression lambdas, including the lambda operator (=>).

## 21.10 Introduction to Functional Programming

### 21.9.2 Assigning Lambdas to Delegate Variables

In line 17 of Fig. 21.7, the lambda expression is assigned to a variable of type NumberPredicate—the delegate type declared in line 9. A delegate can hold a reference to a lambda expression. With traditional methods, a method defined by a lambda expression must have a signature that matches with the delegate type. The NumberPredicate delegate can hold a reference to any method that returns an int and a bool. Based on this, the compiler is able to infer that the lambda expression in line 17 takes an int as an argument and returns a bool result of the expression in its body.

Lines 20–21 display the result of calling the lambda expression defined in line 17. The lambda expression is called via the variable that references it (evenPredicate). Line 24 passes evenPredicate to method FilterArray (lines 49–66), which is identical to the method used in Fig. 21.6—it uses the NumberPredicate delegate to determine whether an array element is included in the result. Lines 27–28 display the filtered results.

### 21.9.3 Explicitly Typed Lambda Parameters

Lambda expressions are often used as methods with delegate-type parameters, but in some cases, you may need to explicitly type the parameters:

```csharp
(int number) => number % 2 == 1
```

This is useful when the compiler cannot infer the type from the context or when you want to be explicit for clarity.

### 21.9.4 Statement Lambdas

Statement lambdas allow you to use blocks of code instead of a single expression:

```csharp
number => {return number > 5}
```

When a lambda uses a statement block, the body is enclosed in curly braces, and if it returns a value, the `return` keyword must be used.
