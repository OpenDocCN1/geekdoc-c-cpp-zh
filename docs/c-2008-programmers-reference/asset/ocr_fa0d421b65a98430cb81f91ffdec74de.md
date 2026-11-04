```
{
    Console.WriteLine("Method 3");
    num1 = 3;
    num2 = 3;
    return 3;
}
```

When the methods delegate is called, Method1(), Method2(), and Method3() are called in succession. However, only the last method (Method3()) returns a value back to the Main() function, as the output shows:

```
Method 1
Method 2
Method 3
3
num1: 3 num2: 3
```

If one of the methods pointed to by a delegate causes an exception, no results are returned. The following modifications to the preceding program shows that Method2() throws an exception and is caught by the Try-Catch block:

```
class Program
{
    delegate int MethodsDelegate(ref int num1, ref int num2);
    static void Main(string[] args)
    {
        int num1 = 0, num2 = 0;
        methodsDelegate = Method1;
        methods += Method2;
        methods += Method3;
```

```
try
{
    //---call the delegated method(s)---
    Console.WriteLine(methods(ref num1, ref num2));
    Console.WriteLine("num1: {0} num2: {1}", num1, num2);
}
catch (Exception ex)
{
    Console.WriteLine(ex.Message);
}

Console.WriteLine("*num1: {0} num2: {1}", num1, num2);
Console.ReadLine();
```

```
static private int Method1(ref int num1, ref int num2)
{
    Console.WriteLine("Method 1");
    num1 = 1;
    num2 = 1;
```