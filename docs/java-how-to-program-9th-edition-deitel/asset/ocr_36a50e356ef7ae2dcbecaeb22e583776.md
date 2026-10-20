# 11.13 (New in Java SE 7) try-with-Resources: Automatic Resource Deallocation

Typically resource-release code should be placed in a finally block to ensure that a resource is released, regardless of whether there were exceptions when the resource was used in the corresponding try block. An alternative notation—the try-with-resources statement (which is new in Java SE 7)—simplifies writing code in which you obtain one or more resources, use them in a try block and release them in a corresponding finally block. For example, a file-processing application (Chapter 17) could process a file with a try-with-resources statement to ensure that the file is closed properly when it’s no longer needed. Each resource must be an object of a class that implements the AutoCloseable interface—such a class has a close method. The general form of a try-with-resources statement is

```
try ( ClassName theObject = new ClassName() )
{
    // use theObject here
}
catch ( Exception e )
{
    // catch exceptions that occur while using the resource
}
```

where ClassName is a class that implements the AutoCloseable interface. This code creates an object of type ClassName and uses it in the try block, then calls its close method to release any resources used by the object. The try-with-resources statement implicitly calls the theObject’s close method at the end of the try block. You can allocate multiple resources in the parentheses following try by separating them with a semicolon (;).

# 11.14 Wrap-Up

In this chapter, you learned how to use exception handling to deal with errors. You learned that exception handling enables you to remove error-handling code from the “main line” of the program’s execution. We showed how to use try blocks to enclose code that may throw an exception, and how to use catch blocks to deal with exceptions that may arise. You learned about the termination model of exception handling, which dictates that after an exception is handled, program control does not return to the throw point. We discussed checked vs. unchecked exceptions, and how to specify with the throws clause the exceptions that a method might throw. You learned how to use the finally block to release resources whether or not an exception occurs. You also learned how to throw and rethrow exceptions. We showed how to obtain information about an exception using methods printStackTrace, getStackTrace and getMessage. Next, we presented chained exceptions, which allow you to wrap original exception information with new exception information. Then, we showed how to create your own exception classes. We introduced preconditions and postconditions to help programmers using your methods understand conditions that must be true when the method is called and when it returns, respectively. When preconditions and postconditions are not met, methods typically throw exceptions. We discussed the assert statement and how it can be used to help you debug your programs. In particular, assert can be used to ensure that preconditions and postconditions