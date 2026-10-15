+   b. An Exception1 exception is thrown by the review.question() method.
+   c. An Exception2 exception is thrown by the review.question() method.
+   d. An Exception3 exception is thrown by the review.question() method.

# 11.4 Exception Propagation

If an exception is not caught and handled where it occurs, control is immediately returned to the method that invoked the method that produced the exception. We can design our software so that the exception is caught and handled at this outer level. If it isn’t caught there, control returns to the method that called it. This process is called propagating the exception. This propagation continues until the exception is caught and handled or until it is passed out of the main method, which terminates the program and produces an exception message. To catch an exception at an outer level, the method that produces the exception must be invoked inside a try block that has catch clauses to handle it.

> KEY CONCEPT
> If an exception is not caught and handled where it occurs, it is propagated to the calling method.

The Propagation program shown in Listing 11.3 succinctly demonstrates the process of exception propagation. The main method invokes method level1 in the ExceptionScope class (see Listing 11.4), which invokes level2, which invokes level3, which produces an exception. Method level3 does not catch and handle the exception, so control is transferred back to level2. The level2 method does not catch and handle the exception either, so control is transferred back to level1. Because the invocation of level2 is made inside a try block (in method level1), the exception is caught and handled at that point.

Note that the output does not include the messages indicating that the methods level3 and level2 are ending. These println statements are never executed, because an exception occurred and had not yet been caught. However, after method level1 handles the exception, processing continues normally from that point, printing the messages indicating that method level1 and the program are ending.

VideoNote
Proper exception handling.

Note also that the catch clause that handles the exception uses the getMessage and printStackTrace methods to output that information. The stack trace shows the methods that were called when the exception occurred.