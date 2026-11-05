# Chapter 123: Func delegates

| Parameter | Details |
|---|---|
| arg or arg1 | the (first) parameter of the method |
| arg2 | the second parameter of the method |
| arg3 | the third parameter of the method |
| arg4 | the fourth parameter of the method |
| T or T1 | the type of the (first) parameter of the method |
| T2 | the type of the second parameter of the method |
| T3 | the type of the third parameter of the method |
| T4 | the type of the fourth parameter of the method |
| TResult | the return type of the method |

# Section 123.1: Without parameters

This example shows how to create a delegate that encapsulates the method that returns the current time

```
static DateTime UTCNow()
{
    return DateTime.UtcNow;
}

static DateTime LocalNow()
{
    return DateTime.Now;
}

static void Main(string[] args)
{
    Func<DateTime> method = UTCNow;
    // method points to the UTCNow method
    // that returns current UTC time
    DateTime utcNow = method();

    method = LocalNow;
    // now method points to the LocalNow method
    // that returns local time

    DateTime localNow = method();
}
```

# Section 123.2: With multiple variables

```
static int Sum(int a, int b)
{
    return a + b;
}

static int Multiplication(int a, int b)
{
    return a * b;
}

static void Main(string[] args)
{
```