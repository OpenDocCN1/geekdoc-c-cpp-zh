# Exception Handling 399

The throw keyword is used to throw an exception. It is followed by a value, such as character string or object, indicating the nature of the exception. The library function notifies the user program by the error by throwing an exception.

The catch keyword is used to catch an exception. A catch-handler block begins with the keyword catch, followed, by a type declaration indicating the type of exception that it catches. That, in turn, is followed by a brace enclosed block of code indicating the actions to take. The catch keyword, along with the exception types, is the point to which control should jump when an exception is thrown.

A try block encompasses the code that is likely to throw an exception. Such a code generally consists of calls to library functions that are designed to throw errors in the manner described herein. One or more catch blocks follow the try block. The 'try' block is indicated by the keyword try followed by a brace—enclosed block of code within which exception will be caught.

The try block looks like this:

```
try // start of try block
{
  z=hmean(x,y);
} // end of try block
```

If any statement in the try block causes an exception, the catch blocks after this block handle the exception.

Exceptions are thrown as follows:

```
if(a==b)
throw "bad hmean( ) arguments : a = -b not allowed";
```

In this case, the exception is the string hmean( ) arguments : a = -b not allowed. The throw statement resembles the return statement because it terminates function execution. Instead, of merely returning to the calling function, a throw causes the control back up through the sequence of current functions until it finds the try block. In this case, the passes program control back to main(). There, the program looks for an exception handler (following the try block) that matches the type of exception.

```
catch (char *) // start of exception handler
cout<<""\n";
cout<<"Enter a new pair of numbers : ";
continue;
} // end of handler
```

The catch keyword identifies the handler and the char * means that this handler catches a string-type exception. The exception is assigned to 's'. Since the exception matches this handler, the program executes the code within the block.

If a program completes executing statements in a try block without any thrown, it skips the catch block or blocks after the try block and goes to the first statement following the handlers.

Let us follow the control of when the values '10' and '–10' are assigned to the hmean(). If the test succeeds and the exception of (char * type) is thrown. the hmean() function terminates. The control goes back to the point where the hmean() function was called and determines whether the call was embedded within a try block or not. It finds that the hmean() function was called from the main() function and that the call was embedded within a try block. The control searches for a catch block that follows the try block and is of the