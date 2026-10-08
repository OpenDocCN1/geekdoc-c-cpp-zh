+   1. System.IO.IOException – this handles I/O errors
2. System.IndexOutOfRangeException – this handles errors generated when a method refers to an array index out of range.
3. System.NullReferenceException – this handles errors generated from deferencing a null object.
4. System.ArrayTypeMismatchException – this handles errors generated when type is mismatched with the array type.
5. System.DivideByZeroException- this handles errors generated from dividing a dividend with zero.
6. System.OutOfMemoryException – this handles errors generated from insufficient free memory.
7. System.InvalidCastException – this handles errors generated during typecasting.
8. System.StackOverflowException – this handles errors generated from stack overflow.

C# provides a structured solution to handle exceptions in the form of catch and try blocks. By using these blocks the core program statements are separated from the error-handling statements and this error handling blocks are implemented using catch, try, throw, and finally keywords.

In C#, you can also define your own exceptions. These are called as user-defined exceptions. The user-defined exception classes are derived from the Exception class.
(Tutorials Point)