(continued)

```
{
    try
    {
        Method2();
    }
    catch (Exception ex)
    {
        throw new Exception(
            "Exception caused by calling Method2() in Method1().", ex);
    }
}

private void Method2()
{
    try
    {
        Method3();
    }
    catch (Exception ex)
    {
        throw new Exception(
            "Exception caused by calling Method3() in Method2().", ex);
    }
}

private void Method3()
{
    try
    {
        int num1 = 5, num2 = 0;
        int result = num1 / num2;
    }
    catch (DivideByZeroException ex)
    {
        throw new Exception('Division by zero' error in Method3().", ex);
    }
}
```

In this program, the Main() function calls Method1(), which in turns calls Method2(). Method2() then calls Method3(). In Method3(), a division-by-zero exception occurs and you rethrow a new Exception exception by passing in the current exception (DividebyZeroException). This exception is caught by Method2(), which rethrows a new Exception exception by passing in the current exception. Method1() in turn catches the exception and rethrows a new Exception exception. Finally, the Main() function catches the exception and prints out the result as shown in Figure 12-4.