# Part I: C# Fundamentals

To lock a block of code, give the lock statement an object as argument. The preceding code could be written as follows:

```
```csharp
class Program
{
    //---used for locking---
    static object obj = new object();

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
            lock (obj)
            {
                balance += 100;
                Console.WriteLine("After crediting, balance is {0}", balance);
            }
        }
    }

    static void Debit()
    {
        //---debit 1000---
        for (int i = 0; i < 10; i++)
        {
            lock (obj)
            {
                balance -= 100;
                Console.WriteLine("After debiting, balance is {0}", balance);
            }
        }
    }
}
```
```

Notice that you first create an instance of an object that will be used for locking purposes:

```
```csharp
//---used for locking---
static object obj = new object();
```
```