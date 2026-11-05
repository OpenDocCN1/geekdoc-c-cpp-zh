Exceptions that occur during destructor execution are worth special mention. If an exception occurs during destructor execution and that exception is not caught, then the execution of that destructor is terminated and the destructor of the base class (if any) is called. If there is no base class (as in the case of the object type) or if there is no base class destructor, then the exception is discarded.

> CHRISTIAN NAGEL The C# compiler creates a finalizer from a destructor. Within the finalizer, a try-finally block is added where the finalizer from the base class is called in the finally block.

# 16.4 Common Exception Classes

The following exceptions are thrown by certain C# operations.

| Exception | Description |
|---|---|
| System.ArithmeticException | A base class for exceptions that occur during arithmetic operations, such as System.DivideByZeroException and System.OverflowException. |
| System.ArrayTypeMismatchException | Thrown when a store into an array fails because the actual type of the stored element is incompatible with the actual type of the array. |
| System.DivideByZeroException | Thrown when an attempt to divide an integral value by zero occurs. |
| System.IndexOutOfRangeException | Thrown when an attempt to index an array via an index that is less than zero or outside the bounds of the array occurs. |
| System.InvalidCastException | Thrown when an explicit conversion from a base type or interface to a derived type fails at runtime. |
| System.NullReferenceException | Thrown when a null reference is used in a way that causes the referenced object to be required. |
| System.OutOfMemoryException | Thrown when an attempt to allocate memory (via new) fails. |