# Chapter 18

In the preceding code, we have defined an indexer that takes two strings, data and replacement Data, as its arguments and replaces a string with replacement Data if the string matches with data. In the Main() method, we have declared the indexer as emp["USA", "United State Of America"] = "Empty". This in turn calls the set accessor or that tries to find the array element that contains the value USA. If it finds one, then USA will be replaced by United State of America. The output of the preceding code is given as follows:

```
Employee[0]: John
Employee[1]: United State of America
Employee[2]: Software Engineer
Employee[3]: 12345
Employee[4]: Developer
```

Let’s now learn how to refer a method.

# Defining Delegates

Delegate is a C# element using which we can refer a method. This is similar to a function pointer that we have already learned in C++. However, a delegate provides type safety; thereby, making it different from a function pointer in C++.

Now, a question arises as why we need delegates in a C# program. Consider a program where we want to refer different methods, which have similar argument types, and whose return patterns are same. In this case, we can use delegates to perform the functionality. In addition, if we want to develop a general algorithm that can be applied for all the data types without writing separate methods for each data type, then we can use delegates for this purpose. Therefore, delegates provide more flexibility in a program to implement any functionality. While using delegates, we need to consider the following points:

+   - Methods only need to be matched with the argument types and return types of the delegate
+   - Delegate allows methods to be passed as a parameter

Delegates are defined at the beginning of the class definition using the delegate keyword. In addition, they must have their delegate handler methods defined in the program. Delegate handler methods are nothing but the methods that matches the argument type and return type of the delegate. Let’s demonstrate the functionality of delegates in Listing 18.15:

**Listing 18.15:** Showing an Example of Delegates

```
using System;
//Defining Delegate
public delegate long Calculator(long item1, long item2);
class Program
{
    public static void Main()
    {
        Items items = new Items(6, 3);
        //Initializing the delegates
        Calculator addition = new Calculator(items.Addition);
        Calculator subtraction = new Calculator(items.Subtraction);
        Calculator multiplication = new Calculator(items.Multiplication);
        Calculator division = new Calculator(items.Division);
        //calling the delegate handler methods using the instance of
        //the delegate
        Console.WriteLine("The result of addition is: "
                          + addition(items.item1, items.item2));
        Console.WriteLine("The result of subtraction is:"
                          + subtraction(items.item1, items.item2));
        Console.WriteLine("The result of multiplication is:"
                          + multiplication(items.item1, items.item2));
```