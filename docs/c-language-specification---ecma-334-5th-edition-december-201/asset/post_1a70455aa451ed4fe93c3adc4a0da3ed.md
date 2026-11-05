
```
delegate void D(int x);
class C
{
    public static void M1(int i) {
        Console.WriteLine("C.M1: " + i);
    }
    public static void M2(int i) {
        Console.WriteLine("C.M2: " + i);
    }

    public void M3(int i) {
        Console.WriteLine("C.M3: " + i);
    }
}
class Test
{
    static void Main() {
        D cd1 = new D(C.M1);
        cd1(-1);    // call M1

        D cd2 = new D(C.M2);
        cd2(-2);    // call M2

        D cd3 = cd1 + cd2;
        cd3(10);    // call M1 then M2

        cd3 += cd1;
        cd3(20);    // call M1, M2, then M1

        C c = new C();
        D cd4 = new D(c.M3);
        cd3 += cd4;
        cd3(30);    // call M1, M2, M1, then M3

        cd3 -= cd1; // remove last M1
        cd3(40);    // call M1, M2, then M3

        cd3 -= cd4;
        cd3(50);    // call M1 then M2

        cd3 -= cd2;
        cd3(60);    // call M1
        cd3 -= cd2; // impossible removal is benign
        cd3(60);    // call M1

        cd3 -= cd1; // invocation list is empty so cd3 is null
        // cd3(70);  // System.NullReferenceException thrown
        cd3 -= cd1; // impossible removal is benign
    }
}
```

As shown in the statement cd3 += cd1;, a delegate can be present in an invocation list multiple times. In this case, it is simply invoked once per occurrence. In an invocation list such as this, when that delegate is removed, the last occurrence in the invocation list is the one actually removed.

Immediately prior to the execution of the final statement, cd3 -= cd1;, the delegate cd3 refers to an empty invocation list. Attempting to remove a delegate from an empty list (or to remove a non-existent delegate from a non-empty list) is not an error.

The output produced is:

```
C.M1: -1
C.M2: -2

C.M1: 10
C.M2: 10

C.M1: 20
C.M2: 20
C.M1: 20

C.M1: 30
C.M2: 30
C.M1: 30
C.M3: 30

C.M1: 40
C.M2: 40
C.M3: 40

C.M1: 50
C.M2: 50

C.M1: 60
C.M1: 60
```

end example]

## 21. Exceptions

### 21.1 General

Exceptions in C# provide a structured, uniform, and type-safe way of handling both system-level and application-level error conditions.

### 21.2 Causes of exceptions

An exception can be thrown in two different ways.

- A throw statement (§13.10.6) throws an exception immediately and unconditionally. Control never reaches the statement immediately following the throw.
- Certain exceptional conditions that arise during the processing of C# statements and expressions cause an exception in certain circumstances when the operation cannot be completed normally. [Example: An integer division operation (§12.9.3) throws a System.DivideByZeroException if the denominator is zero. end example] See §21.5 for a list of the various exceptions that can occur in this way.

### 21.3 The System.Exception class

The System.Exception class is the base type of all exceptions. This class has a few notable properties that all exceptions share:

- Message is a read-only property of type string that contains a human-readable description of the reason for the exception.
- InnerException is a read-only property of type Exception. If its value is non-null, it refers to the exception that caused the current exception. (That is, the current exception was raised in a catch block handling the InnerException.) Otherwise, its value is null, indicating that this exception was not caused by another exception. The number of exception objects chained together in this manner can be arbitrary.

The value of these properties can be specified in calls to the instance constructor for System.Exception.

### 21.4 How exceptions are handled

Exceptions are handled by a try statement (§13.11).

When an exception occurs, the system searches for the nearest catch clause that can handle the exception, as determined by the run-time type of the exception. First, the current method is searched for a lexically enclosing try statement, and the associated catch clauses of the try statement are considered in order. If that fails, the method that called the current method is searched for a lexically enclosing try statement. This search continues until a catch clause is found that can handle the current exception, by naming an exception class that is of the same class, or a base class, of the run-time type of the exception being thrown. A catch clause that doesn't name an exception class can handle any exception.

Once a matching catch clause is found, the system prepares to transfer control to the first statement of the catch clause. Before execution of the catch clause begins, the system first executes, in order, any finally clauses that were associated with try statements more nested than the one that caught the exception.

If no matching catch clause is found:

- If the search for a matching catch clause reaches a static constructor (§15.12) or static field initializer, then a System.TypeInitializationException is thrown at the point that triggered the invocation of the static constructor. The inner exception of the System.TypeInitializationException contains the exception that was originally thrown.
- Otherwise, if an exception occurs during finalizer execution, and that exception is not caught, then the behavior is unspecified.
- Otherwise, if the search for matching catch clauses reaches the code that initially started the thread, then execution of the thread is terminated. The impact of such termination is implementation-defined.

### 21.5 Common exception classes

The following exceptions are thrown by certain C# operations.

| Exception | Description |
|---|---|
| System.ArithmeticException | A base class for exceptions that occur during arithmetic operations, such as System.DivideByZeroException and System.OverflowException. |
| System.ArrayTypeMismatchException | Thrown when a store into an array fails because the type of the stored element is incompatible with the type of the array. |
| System.DivideByZeroException | Thrown when an attempt to divide an integral value by zero occurs. |
| System.IndexOutOfRangeException | Thrown when an attempt to index an array via an index that is less than zero or outside the bounds of the array. |
| System.InvalidCastException | Thrown when an explicit conversion from a base type or interface to a derived type fails at run-time. |
| System.NullReferenceException | Thrown when a null reference is used in a way that causes the referenced object to be required. |
| System.OutOfMemoryException | Thrown when an attempt to allocate memory (via new) fails. |
| System.OverflowException | Thrown when an arithmetic operation in a checked context overflows. |
| System.StackOverflowException | Thrown when the execution stack is exhausted by having too many pending calls; typically indicative of very deep or unbounded recursion. |
| System.TypeInitializationException | Thrown when a static constructor or static field initializer throws an exception, and no catch clause exists to catch it. |

## 22. Attributes

### 22.1 General

Much of the C# language enables the programmer to specify declarative information about the entities defined in the program. For example, the accessibility of a method in a class is specified by decorating it with the method-modifiers public, protected, internal, and private.

C# enables programmers to invent new kinds of declarative information, called attributes. Programmers can then attach attributes to various program entities, and retrieve attribute information in a run-time environment. [Note: For instance, a framework might define a HelpAttribute attribute that can be placed on certain program elements (such as classes and methods) to provide a mapping from those program elements to their documentation. end note]

Attributes are defined through the declaration of attribute classes (§22.2), which can have positional and named parameters (§22.2.3). Attributes are attached to entities in a C# program using attribute specifications (§22.3), and can be retrieved at run-time as attribute instances (§22.4).

### 22.2 Attribute classes

#### 22.2.1 General

A class that derives from the abstract class System.Attribute, whether directly or indirectly, is an attribute class. The declaration of an attribute class defines a new kind of attribute that can be placed on program entities. By convention, attribute classes are named with a suffix of Attribute. Uses of an attribute may either include or omit this suffix.

A generic class declaration shall not use System.Attribute as a direct or indirect base class. [Example:

```
using System;
public class B : Attribute {}
public class C<T> : B {}  // Error - generic cannot be an attribute
```

end example]

#### 22.2.2 Attribute usage

The attribute AttributeUsage (§22.5.2) is used to describe how an attribute class can be used.

AttributeUsage has a positional parameter (§22.2.3) that enables an attribute class to specify the kinds of program entities on which it can be used. [Example: The example

```
using System;
[AttributeUsage(AttributeTargets.Class | AttributeTargets.Interface)]
public class SimpleAttribute: Attribute
{ ... }
```
