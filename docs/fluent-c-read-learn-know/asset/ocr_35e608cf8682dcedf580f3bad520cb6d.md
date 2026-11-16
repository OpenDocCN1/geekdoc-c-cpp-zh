![](bbox=[0.09, 0.05, 0.21, 0.21])

# PUT ON YOUR THINKING HAT

I've been talking, talking, talking at you. Time for you to go to work.

Assume that MyObject.MyMethod() can throw one of two exceptions: a base Exception or a ParseException. Write a code snippet that wraps a call to MyMethod() in a try..catch block, displays the Message property of a ParseException in a MessageBox and re-throws a general Exception.

The exception classes expose a Message property that contains a user-readable description of the problem that occurred, but the names themselves also tell you a great deal. Under what circumstances do you think each of these exceptions might be thrown?

+   - DivideByZeroException
+   - ArgumentException
+   - OverflowException
+   - NotImplementedException