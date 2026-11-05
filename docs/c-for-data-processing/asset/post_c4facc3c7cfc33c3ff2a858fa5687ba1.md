
```csharp
using System;
class MethodDemo
{
    static void doit()
    {
        Console.WriteLine("Hello");
    }
    public static void Main()
    {
        doit();
        doit();
    }
}
```

In the main method I make two calls of doit. Each time I call the method the code in the block which is the body of the method is executed. In this case it contains a single statement which prints "Hello" on the console. The result of running the above program would be:

```
Hello
Hello
```

So, we can use methods to save us from writing the same code twice. We simply put the code inside a method body and then call it when we need it.

## 3.1.2 Parameters

At this point methods are useful because they let us use the same block of statements at many points in the program. However, they become more useful if we allow them to have parameters.

A parameter is a means of passing a value into a method call. The method is given the data to work on. As an example, consider the code below:

```csharp
using System;
class MethodDemo
{
    static void silly(int i)
    {
        Console.WriteLine("i is : " + i);
    }
    public static void Main()
    {
        silly(101);
        silly(500);
    }
}
```

The method silly has a single integer parameter. Within the block of code which is the body of this method we can use the parameter i as an integer variable. When the method starts the value supplied for the parameter is copied into it. This means that when the program runs we get output like this:

```
i is : 101
i is : 500
```

## 3.1.3 Return values

A method can also return a value to the caller. You have already used this feature, the methods ReadLine and Parse both return results that we have used in our programs:

```csharp
using System;

class ReturnDemo
{
    static int sillyReturnPlus(int i)
    {
        i = i + 1;
        Console.WriteLine("i is : " + i);
        return i;
    }

    public static void Main()
    {
        int res;
        res = sillyReturnPlus(5);
        Console.WriteLine("res is : " + res);
    }
}
```

The method sillyReturnPlus takes the value of the parameter and returns it plus one.

The value that a method returns can be used anywhere in a program where a variable of that type could be used. In other words a call of sillyReturnPlus can take the place of an integer. See if you can work out what this code would display:

```csharp
res = sillyReturnPlus(5) + sillyReturnPlus(7) + 1;
Console.WriteLine("res is : " + res);
```

It is actually OK to ignore the value returned by a method, but this is actually a rather pointless thing to do:

```csharp
sillyReturnPlus(5); // will compile but do nothing useful
```

## 3.1.4 A Useful Method

Now we can start to write genuinely useful methods:

```csharp
static double readValue(
    string prompt, // prompt for the user
    double low,    // lowest allowed value
    double high    // highest allowed value
)
{
    double result = 0;
    do
    {
        Console.WriteLine(prompt +
            " between " + low +
            " and " + high);
        string resultString = Console.ReadLine();
        result = double.Parse(resultString);
    } while ((result < low) || (result > high));
    return result;
}
```

The readValue method is told the prompt to use and the lowest and the highest allowed values. It can then be used to read values and make sure that they are in range. We can use this method to read anything and make sure that the value supplied is within a particular range.

```csharp
double windowWidth = readValue(
    "Enter width of window: ", MIN_WIDTH, MAX_WIDTH);

double age = readValue("Enter your age: ", 0, 70);
```

The first call of readValue gets the width of a window. The second reads an age between 0 and 70.

### Programmer's Point: Design with methods

Methods are a very useful part of the programmer's toolkit. They form an important part of the development process. Once you have worked out what the customer wants and gathered your metadata you can start thinking about how you are going to break the program down into methods. Often you find that as you write the code you are repeating a particular action. If you do this you should consider taking that action and moving it into a method. There are two reasons why this is a good idea:

- 1. It saves you writing the same code twice.
- 2. If a fault is found in the code you only have to fix it in one place.

Moving code around and creating methods is called refactoring. This will be an important part of the Software Engineering we do later.

### Method Limitations

A method is very good for getting work done, but it can be a bit limited because of the way it works. For example, if I want to write a method which reads in the name and the age of a person I have a problem. From what we have seen of methods, they can only return one value. So I could write a method which returns the name of a person, or write one which returns an age. But I can't write a method which returns both values at the same time as a method can only return one value. As you will find out when you try, changing the value of a parameter does not change the value of the thing passed in. This is because, unless you specify otherwise, only the value of a parameter is passed into a call to a method.

## 3.1.5 Parameter Passing By Value

So, what do I mean by "passing parameters by value"? Consider:

```csharp
static void addOneToParam(int i)
{
    i = i + 1;
    Console.WriteLine("i is : " + i);
}
```

The method addOneToParam adds one to the parameter; prints the result out and then returns:

```csharp
int test = 20;
addOneToParam(test);
Console.WriteLine("test is : " + test);
```

The piece of C# above calls the method with the variable test as the parameter. When it runs it prints out the following:

```
i is : 21
test is : 20
```

It is very important that you understand what is happening here. The value of test is being used in the call of addOneToParam. The program works out the result of the expression to be passed into the method call as a parameter. It then passes this value into the call. This means that you can write calls like:

```csharp
test = 20;
addOneToParam(test + 99);
```

This would print out:

```
i is : 120
```

Pass by value is very safe, because nothing the method does can affect variables in the code which calls it. However, it is a limitation when we want to create a method which returns more than one value.

## 3.1.6 Parameter Passing By Reference

*It is very important that you understand how references work. If you don’t understand these you can’t call yourself a proper programmer!*

Fortunately C# provides a way that, rather than sending the value of a variable into a method, a reference to that variable is supplied instead. Inside the method, rather than using the value of the variable the reference is used to get the actual variable itself. Effectively the thing that is passed into the method is the position or address of the variable in memory, rather than the content of the variable.

So, rather than passing in “20” in our above call the compiler will generate code which passes in “memory location 5023” instead (assuming that the variable test is actually stored at 5023). This memory location is used by the method, instead of the value. In other words:

> “If you pass by reference, changes to the parameter change the variable whose reference you passed”

If you find references confusing you are not alone. However, we use them in real life all the time with no problems. If you say “Deliver the carpet to 23 High Street,” you are giving the delivery man a reference. Using a reference in a program is just the same. The program will say “Get the value from location 5023” rather than “The value is 1”.

Consider the code:

```csharp
static void addOneToRefParam(ref int i)
{
    i = i + 1;
    Console.WriteLine("i is: " + i);
}
```

Note that the keyword ref has been added to the information about the parameter.

```csharp
test = 20;
addOneToRefParam(ref test);
Console.WriteLine("test is: " + test);
```

The code above makes a call to the new method, and also has the word ref in front of the parameter. In this case the output is as follows:

```
i is 21
test is: 21
```

In this case the method call has made changes to the content of the variable. Note that C# is careful about when a parameter is a reference. You have to put the word ref in the method heading and also in the call of the method.

### Programmer's Point: Document your side-effects

A change by a method to something around it is called a side effect of the method. In other words, when someone calls our addOneToRefParam method, it is going to have the “side effect” of changing something outside the method itself (namely the value of the parameter passed by reference).

Generally speaking you have to be careful with side effects, as someone reading your program has to know that your method has made changes in this way.

## 3.1.7 Passing Parameters as "out" references

When you pass a parameter as a reference you are giving the method complete control of it. Sometimes you don’t want this. Instead you want to just allow the method to change the variable. This is the case when we want to read in the name and age of a user. The original value of the parameters is of no interest to the method. Instead it just wants to deliver results to them. In this case I can replace the ref with the keyword out:
