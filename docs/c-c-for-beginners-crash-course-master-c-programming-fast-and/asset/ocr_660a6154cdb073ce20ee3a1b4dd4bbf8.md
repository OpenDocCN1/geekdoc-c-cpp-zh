# 13.4 Exception classes in C#

There are several exception classes which are directly or indirectly derived from the **System.Exception** class. Some of the classes that are derived from the **System.Exception** class are **System.ApplicationException** and **System.SystemException** classes.

For a user-defined application having its own exception, the exception must be inherited from the **ApplicationException** class.

The **System.SystemException** class is the base class for all exceptions.

| Exception class | Description |
|---|---|
| System.IO.IOException | It handles the I/O Errors |
| System.NullReferenceException | Errors generated during the process of dereferencing a null object |
| System.IndexOutOfRangeException | Errors generated when a method refers an array element out of bound |
| System.DivideByZeroException | Errors generated during the process of dividing the dividend by zero |
| System.OutOfMemoryException | Memory allocation to the application errors |
| System.InvalidCastException | Errors due to type casting |
| System.StackOverflowException | The errors generated due to stack overflow |