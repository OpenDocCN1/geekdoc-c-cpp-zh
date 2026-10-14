# Note

If you drop into the Visual Studio debugger, you have probably enabled Visual Studio to catch all common language runtime exceptions as they are thrown. If this happens, on the Debug menu, click Continue. Remember to disable Visual Studio from catching CLR exceptions as they are thrown when you have finished this exercise!

+   4. Return to Visual Studio and stop debugging.

The application is now a lot more robust. However, several exceptions could still arise that are not caught and will cause the application to fail. For example, if you attempt to divide by 0, an unhandled *DivideByZeroException* will be thrown. (Integer division by 0 does throw an exception, unlike floating-point division by 0.) One way to solve this problem is to write an ever larger number of *catch* handlers inside the *calculateClick* method. Another solution is to add a general *catch* handler that catches *Exception* at the end of the list of *catch* handlers. This will trap all unexpected exceptions that you might have forgotten about or that might be caused as a result of truly unusual circumstances.

# Note

Using a catchall handler to trap the *Exception* exception is not an excuse to omit catching specific exceptions. The more definite you can be in your exception handling, the easier it will be to maintain your code and spot the causes of any underlying or commonly recurring issues. Only use the *Exception* exception for cases that are really... well, exceptional. For the purposes of the following exercise, the “divide by zero” exception falls into this category. However, having established that this exception is a distinct possibility in a professional application, good practice would be to add a handler for the *DivideByZeroException* exception to the application.

# Catch unhandled exceptions

+   1. In the Code and Text Editor window displaying MainPage.xaml.cs, add the following *catch* handler to the end of the list of existing *catch* handlers in the *calculateClick* method:

Click here to view code image

```
catch (Exception ex)
{
    result.Text = ex.Message;
```