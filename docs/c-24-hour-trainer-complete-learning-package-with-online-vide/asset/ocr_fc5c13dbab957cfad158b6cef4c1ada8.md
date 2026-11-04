The method takes as a parameter the distance it should move. It uses the Turtle's current position and direction to figure out where this move will finish. It uses some graphics code to draw a line from the current position to the new one (don't worry about the details) and finishes by saving the new position.

# EVENTS

Events let the class tell the rest of the program that something interesting is happening. For example, if a BankAccount object's balance falls below 0, it could raise an AccountOverdrawn event to notify the main program.

Declaring an event in C# is a bit tricky because you first need to understand delegates.

# Delegates

A delegate is a data type that can hold a specific kind of method. For example, you could make a delegate type that represents methods that take no parameters and return a double. You could then declare a variable of that type and save a method in it.

Confusing? You bet!

The key to understanding delegates is to remember that a delegate type is a new data type just like a string or int. The difference is that a variable with a delegate type holds a method, not a simple value like "Hello" or 27.

The Delegates example program, which is part of this lesson's download on the book's website, provides a simple example. The program uses four steps to demonstrate delegates: declare the delegate type, create variables of that type, initialize the variables, and use the variables' values.

First the program defines a delegate type:

```
// Define a delegate type that takes no parameters and returns nothing.
private delegate void DoSomethingMethod();
```

The declaration begins with the accessibility keyword private and then the keyword delegate to tell C# that it is defining a delegate type. The rest of the declaration gives the delegate type's name DoSomethingMethod. It also indicates that instances of this type must refer to methods that take no parameters and return nothing (void).

Now that it has defined the delegate type, the code declares three variables of that type. Each of the variables can hold a reference to a method that takes no parameters and returns nothing:

```
// Declare three DoSomethingMethod variables.
private DoSomethingMethod method1, method2, method3;
```

Next the program defines two methods that match the delegate's definition:

```
// Define some methods that have the delegate's type.
private void SayHi()
{
    MessageBox.Show("Hi");
}
```