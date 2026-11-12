> Note: If an exception occurs in the middle of a try block, the destructors of all objects local to that block are called. This ensures that all resources allocated in that block are released, even if the block is not completely executed. In general, you should not use the new operator inside of a try block. An exception will complicate knowing whether memory was allocated and, if it was, whether it was deallocated.

> Programming Tip: An important implementation detail of a try block is that it should contain as few statements as possible—ideally, only the statement that could throw an exception. Keeping the try block small reduces the risk of either important code not being executed or allocated memory not being deallocated if an exception is thrown.

The syntax for a catch block resembles that of a function definition. It specifies both the type of exception the catch block will handle and an identifier. This identifier—called a catch block parameter—provides a name for the caught exception that can be used within the catch block. Although a catch block is not a function, throwing an exception is like calling a catch block as if it were a function. The catch block parameter represents the actual exception object provided by the throw statement.

The steps taken in the catch block vary from situation to situation and can be as simple as either doing nothing or displaying an error message, or as elaborate as tests that update variables and retry the function that threw the exception. Every exception class in the C++ Standard Library defines the accessor method what, which returns a descriptive string created when the exception is thrown. The body of the catch block can display this string to provide an indication of the nature of the exception.

> Note: A catch block whose parameter has the type ExceptionClass can catch exceptions of the class ExceptionClass and any of ExceptionClass's descendant classes. Specifying a catch block with a parameter of type exception catches any exception that can be thrown.

Listing C3-4 shows sample code that calls our findBox function and catches any logic_error exception thrown. The catch block displays a message to the user that something unusual has happened and creates a PlainBox object for findBox so that the statement following the catch block executes correctly.

```
LISTING C3-4 Trying the function findBox
// Create and initialize an array of boxes
PlainBox<string> myBoxes[5]; // Array of PlainBox objects
myBoxes[0] = PlainBox<string>("ring");
myBoxes[1] = PlainBox<string>("hat");
myBoxes[2] = PlainBox<string>("skirt");
myBoxes[3] = PlainBox<string>("sock");
myBoxes[4] = PlainBox<string>("shoe");
PlainBox<string> findBox;
```