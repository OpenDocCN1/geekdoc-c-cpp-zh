
What caused these exceptions to be thrown? The first output in Figure 12-15 is generated because of an attempt to divide by zero. The second one threw an "Index outside the bounds of the array" exception. No message of "Index outside the bounds of the array" is displayed in response to a bug in the program. The exception was thrown when the statement that computes the average from Example 12-2 was changed to the statement shown in Example 12-3.

### Example 12-3

```csharp
averageTestScore = totalScores / examScore[10]; // Invalid
```

There is no `examScore[10]`. Example 12-2 had the correct arithmetic statement; the divisor should be `countOfScores`.

```csharp
averageTestScore = totalScores / countOfScores; // Correct
```

![](img/e33ae760e23d89eac66541252ad65de8_774_0.png)

The computation was modified to illustrate that programmer mistakes (bugs) can lead to exceptions being thrown.

Although you can keep the program from terminating abnormally by using a generic `catch` clause, you can debug more easily if you know what caused the exception to be thrown. Just displaying a message saying there is a problem does not help a lot.

## Exception Object

When an exception is raised with .NET languages, an `object` is created to represent the exception. All exception objects inherit from the `base class` for exceptions, named `Exception`. It is part of the `System` namespace. An exception `object`, like other objects, has properties and behaviors (methods). The `catch` clause may list an exception `class` name, and an `object` identifier inside parentheses following the `catch` keyword as shown in Example 12-4. Actually to use any of the properties of the exception `object` that is created, you must have an `object` name. Using the `catch { }` without an exception type does not give you access to an `object`.

One of the properties of the exception `base class` is `Message`. Message returns a `string` describing the exception. Because it is a property of the `base class`, it can be used with any exception `object`. Example 12-4 includes the Exception `class` in the argument list for the `catch` clause. The `object` identifier is used to name an `object` of that `class`. The `object` can now be used with any of the properties or methods of the Exception `class`. The Message property, associated with `object`, is used inside the `catch` clause to display a message describing the exception.

![](img/e33ae760e23d89eac66541252ad65de8_774_1.png)

You cannot use the Message property or any of the other members of the `class` without an `object`. This is one reason the argument list (`System.Exception e`) needs to be included.

### Example 12-4

```csharp
catch (System.Exception e)
{
    Console.Error.WriteLine("Problem with scores - " +
        "Cannot compute average");
    Console.Error.WriteLine(e.Message);
}
```

No filtering of exceptions occurs by adding the `(System.Exception e)` for the argument list. Any exception that is thrown in this method is caught because all exceptions are derived from this base `System.Exception` class. The advantage of typing the argument list is that you have an object identifier to use with properties.

In Example 12-4, in addition to displaying the programmer-supplied message indicating there is a problem, an additional string, "Index was outside the bounds of the array," is displayed. That is the current value of the `Message` property for `e` object. Both of these strings are displayed on the Error output device. Now if the application is run again and it still contains the programmer error previously entered, the output lists what caused the exception to be thrown, as shown in Figure 12-16.

![](img/e33ae760e23d89eac66541252ad65de8_775_0.png)

**Figure 12-16** Use of Message property with the exception object

Calls were made to the `Console.Error.WriteLine()` method to illustrate that it is probably more appropriate to display error messages to the Error output device. By default, its output goes to the console screen, just as it does for Console class output. However, the Error output device can be changed to display to a different device.

The argument list is normally included to filter the exceptions. By specifying more than one exception filter, you can write code in the catch clauses that is specific to the particular exception thrown. To do that, you have to know more about the different exception classes that make up the .NET Framework class library, and the next section discusses some of them.

## Exception Classes

When an error occurs, it is reported by creating and throwing an `object` that corresponds to the specific type of exception that is thrown. The `object` contains information about the error. There are a number of different types of exceptions that can be thrown.

### Derived Classes of the Base Exception Class

Table 12-1 shows some of the derived classes of the base `Exception` class. The `ApplicationException` and `SystemException` classes form the basis for run-time exceptions and are discussed following Table 12-1.

**Table 12-1** Derived classes of the base Exception class

| Classes that inherit from Exception |
|---|
| `Microsoft.Build.BuildEngine.InvalidProjectFileException` |
| `Microsoft.WindowsMobile.DirectX.DirectXException` |
| `System.ApplicationException` |
| `System.ComponentModel.Design.ExceptionCollection` |
| `System.Configuration.SettingsPropertyIsReadOnlyException` |
| `System.IO.IsolatedStorage.IsolatedStorageException` |
| `System.Runtime.Remoting.MetadataServices.SUDSGeneratorException` |
| `System.Runtime.Remoting.MetadataServices.SUDSParserException` |
| `System.SystemException` |
| `System.Windows.Forms.AxHost.InvalidActiveXStateException` |

From Table 12-1, the two exception classes of interest are the `ApplicationException` and `SystemException` classes. The other classes listed in the table are not discussed in this chapter; however, you are encouraged to explore the MSDN documentation to learn more about them.

### ApplicationException Class

You can write your own exception classes or use one of the many supplied .NET exception classes. The `ApplicationException` exception was included by the designers of .NET to enable a distinction to be made between user-defined exceptions and exceptions defined by the system. If you write your own exceptions, they should derive from `ApplicationException`. The `ApplicationException` exception is thrown by a user program, not the CLR.

### SystemException Class

The system-supplied exception classes for run-time exceptions derive mainly from the SystemException class. SystemException adds no functionality to classes. Except for its constructor, the SystemException class has no additional properties or methods other than those derived from the Exception and Object classes. The Exception class has several properties. You have already seen the results of two of them—Message and StackTrace. StackTrace returns a string that contains the call trace of methods. The Message property provides details about the cause of the exception. Another property of the Exception class, HelpLink, can contain a URL to a Help file that can provide additional information about the cause of the exception. The Source property gets or sets the name of the application or the object that caused the error, and the TargetSite property gets the method that threw the exception.

Over 70 classes derive from the SystemException class. Table 12-2 lists a few of the more common exceptions that are thrown. You might want to consider adding handlers to catch many of these.

**Table 12-2** Derived classes of SystemException

| Exception classes derived from the SystemException class | Description of circumstances causing an exception to be thrown |
|---|---|
| System.ArgumentException | One of the arguments provided to a method is invalid. |
| System.ArithmeticException | There are errors in an arithmetic, casting, or conversion operation. Has derived members of System.DivideByZeroException and System.OverflowException. |
| System.ArrayTypeMismatchException | An attempt is made to store an element of the wrong type within an array. |
| System.FormatException | The format of an argument does not meet the parameter specifications. |
| System.IndexOutOfRangeException | An attempt is made to access an element of an array with an index that is outside the bounds of the array. |
| System.InvalidCastException | There is invalid casting or explicit conversion. |
| System.IO.IOException | An I/O error occurs. |
| System.NullReferenceException | There is an attempt to dereference a null object reference. |
| System.OutOfMemoryException | There is not enough memory to continue the execution of a program. |
| System.RankException | An array with the wrong number of dimensions is passed to a method. |
