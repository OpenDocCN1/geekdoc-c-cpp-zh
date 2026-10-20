# Good Programming Practice 11.3

Associating each type of serious execution-time malfunction with an appropriately named Exception class improves program clarity.

# Software Engineering Observation 11.12

When defining your own exception type, study the existing exception classes in the Java API and try to extend a related exception class. For example, if you’re creating a new class to represent when a method attempts a division by zero, you might extend class ArithmeticException because division by zero occurs during arithmetic. If the existing classes are not appropriate superclasses for your new exception class, decide whether your new class should be a checked or an unchecked exception class. The new exception class should be a checked exception (i.e., extend Exception but not RuntimeException) if clients should be required to handle the exception. The client application should be able to reasonably recover from such an exception. The new exception class should extend RuntimeException if the client code should be able to ignore the exception (i.e., the exception is an unchecked one).

In Chapter 22, Custom Generic Data Structures, we provide an example of a custom exception class. We declare a reusable class called List that’s capable of storing a list of references to objects. Some operations typically performed on a List are not allowed if the List is empty, such as removing an item from the front or back of the list. For this reason, some List methods throw exceptions of exception class EmptyListException.

# Good Programming Practice 11.4

By convention, all exception-class names should end with the word Exception.

# 11.10 Preconditions and Postconditions

Programmers spend significant amounts of time maintaining and debugging code. To facilitate these tasks and to improve the overall design, you can specify the expected states before and after a method’s execution. These states are called preconditions and postconditions, respectively.

A precondition must be true when a method is invoked. Preconditions describe constraints on method parameters and any other expectations the method has about the current state of a program just before it begins executing. If the preconditions are not met, then the method’s behavior is undefined—it may throw an exception, proceed with an illegal value or attempt to recover from the error. You should not expect consistent behavior if the preconditions are not satisfied.

A postcondition is true after the method successfully returns. Postconditions describe constraints on the return value and any other side effects the method may have. When defining a method, you should document all postconditions so that others know what to expect when they call your method, and you should make certain that your method honors all its postconditions if its preconditions are indeed met.

When their preconditions or postconditions are not met, methods typically throw exceptions. As an example, examine String method charAt, which has one int parameter—an index in the String. For a precondition, method charAt assumes that index is