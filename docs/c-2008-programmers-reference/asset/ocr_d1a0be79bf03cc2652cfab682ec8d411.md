# ## Using Interlocked Class

Because incrementing and decrementing are such common operations in programming, the .NET Framework class library provides the `Interlocked` class for performing atomic operations for variables that are shared by multiple threads. You can rewrite the preceding example using the `Increment()` method from the static `Interlocked` class:

```
```csharp
static void IncrementVar()
{
    Interlocked.Increment(ref _value);
}
```
```

You need to pass in the variable to be incremented by reference to the `Increment()` method. When a thread encounters the `Increment()` statement, all other threads executing the same statement must wait until the incrementing is done.

The `Interlocked` class also includes the `Decrement()` method that, as its name implies, decrements the specified variable by one.

# ## Using C# Lock

The `Interlocked` class is useful when you are performing atomic increment or decrement operations. What happens if you have multiple statements that you need to perform atomically? Take a look at the following program:

```
```csharp
class Program
{
    //---initial balance amount---
    static int balance = 500;

    static void Main(string[] args)
    {
        Thread t1 = new Thread(new ThreadStart(Debit));
        t1.Start();

        Thread t2 = new Thread(new ThreadStart(Credit));
        t2.Start();

        Console.ReadLine();
    }

    static void Credit()
    {
        //---credit 1500---
        for (int i = 0; i < 15; i++)
        {
            balance += 100;
            Console.WriteLine("After crediting, balance is {0}", balance);
        }
    }

    static void Debit()
```
```