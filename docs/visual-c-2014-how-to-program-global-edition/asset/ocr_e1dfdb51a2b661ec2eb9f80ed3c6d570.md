# 10.3 Controlling Access to Members 439

# Calling Time Method SetTime with Invalid Values

To illustrate that method SetTime validates its arguments, line 30 calls SetTime with invalid arguments of 99 for the hour, minute and second. This statement is placed in a try block (lines 28–31) in case SetTime throws an ArgumentOutOfRangeException, which it will do since the arguments are invalid. When this occurs, the exception is caught at lines 32–35 and the exception'sMessage property is displayed. Lines 38–40 put the time again in both formats to confirm that SetTime did not change the time when invalid arguments were supplied.

Notes on Time1 Class Declaration
Consider several class-design ideas with respect to Time1. The time is represented as three integers for the hour, minute and second. However, the actual data representation used within the class is of no concern to the client's class. For example, it would be perfectly reasonable for Time to represent the time internally as the number of seconds since midnight or the number of minutes and seconds since midnight. Clients could use the public methods and properties to get the result without being aware of this—course, the Hour, Minute and Second properties would need to be reworked with the new data representation. (Exercise 10.4 asks the user to represent the number of seconds since midnight and that indeed no change is visible to the client of the class.)

![](bbox=[0.143, 0.467, 0.218, 0.563])

Software Engineering Observation 10.1
Classes simply programming because the client can use only the public members exposed by the class. Classes are usually client oriented rather than implementation oriented. Clients are neither aware of, nor involved in, class implementation. Clients generally care about what the class does but not how the class does. Clients do, of course, care that the class operates correctly and efficiently.

![](bbox=[0.143, 0.577, 0.218, 0.672])

Software Engineering Observation 10.2
Interfaces change less frequently than implementations. When an implementation-dependent code must change accordingly. Hiding the possibility that other parts of the app become dependent on class-implementation details.

![](bbox=[0.143, 0.686, 0.218, 0.78])

Software Engineering Observation 10.3
Date and time manipulations are more complex than the simplified classes we use in this book. For applications that require date and time checking, check out .NET DateTime-Offset, DateTime, TimeSpan and TimeZone value types in namespace System.

# 10.3 Controlling Access to Members

The access modifies public and private access to a class's variables, methods and properties. (In Chapter 11, we will introduce the additional access modifier protected.) As we stated in Section 10.2, the primary purpose of public methods and properties is to present to the clients a view of the class that provides (the class's public interface). Clients of the class need not be concerned with how the class accomplishes its tasks. For reason, a class's private variables, properties and methods (i.e., the class's implementation details) are not directly accessible to the class's clients.