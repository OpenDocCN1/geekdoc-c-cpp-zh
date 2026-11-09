By the way, it is OK to catch `System.Exception` and execute some code inside the `catch` block’s braces as long as you re-throw the exception at the bottom of that code. Catching `System.Exception` and swallowing the exception (not re-throwing it) should never be done because it hides failures that allow the application to run with unpredictable results and potential security vulnerabilities. Visual Studio’s code analysis tool (FxCopCmd.exe) will flag any code that contains a `catch (Exception)` block unless there is a `throw` statement included in the block’s code. The “Backing Out of a Partially Completed Operation When an Unrecoverable Exception Occurs—Maintaining State” section, coming shortly in this chapter, will discuss this pattern.

Finally, it is OK to catch an exception occurring in one thread and re-throw the exception in another thread. The Asynchronous Programming Model (discussed in Chapter 27, “I/O-Bound Asynchronous Operations”) supports this. For example, if a thread pool thread executes code that throws an exception, the CLR catches and swallows the exception and allows the thread to return to the thread pool. Later, some thread should call an `EndXxx` method to determine the result of the asynchronous operation. The `EndXxx` method will throw the same exception object that was thrown by the thread pool thread that did the actual work. In this scenario, the exception is being swallowed by the first thread; however, the exception is being re-thrown by the thread that called the `EndXxx` method, so it is not being hidden from the application.

# ## Recovering Gracefully from an Exception

Sometimes you call a method knowing in advance some of the exceptions that the method might throw. Because you expect these exceptions, you might want to have some code that allows your application to recover gracefully from the situation and continue running. Here’s an example in pseudocode:

```
```
public String CalculateSpreadsheetCell(Int32 row, Int32 column) {
    String result;
    try {
        result = /* Code to calculate value of a spreadsheet’s cell */ ;
    }
    catch (DivideByZeroException) {
        result = "Can't show value: Divide by zero";
    }
    catch (OverflowException) {
        result = "Can't show value: Too big";
    }
    return result;
}
```
```

This pseudocode calculates the contents of a cell in a spreadsheet and returns a string representing the value to the caller so that the caller can display the string in the application’s window. However, a cell’s contents might be the result of dividing one cell by another cell. If the cell containing the denominator contains 0, the CLR will throw a `DivideByZeroException` object. In this case, the method catches this specific exception and returns a special string that