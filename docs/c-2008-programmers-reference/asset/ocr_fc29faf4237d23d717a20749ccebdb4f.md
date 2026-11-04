![](bbox=[0.22, 0.13, 0.8, 0.37])

Figure 12-4

If you set a breakpoint in the catch block within the Main() function, you will see that the InnerException property contains details of each exception and that all the exceptions are chained via the InnerException property (see Figure 12-5).

![](bbox=[0.24, 0.55, 0.78, 0.75])

Figure 12-5

# Using Exception Objects

Instead of using the default description for each exception class you are throwing, you can customize the description of the exception by creating an instance of the exception and then setting the Message property. You can also specify the HelpLink property to point to a URL where developers can find more information about the exception. For example, you can create a new instance of the ArithmeticException class using the following code:

```
if (num1 == 0)
{
    ArithmeticException ex =
        new ArithmeticException("Value of num1 cannot be 0.")
    {
        HelpLink = "http://www.learn2develop.net"
    };
    throw ex;
}
```