So, it’s important to have a good error handling strategy in place that enables you to avoid errors when possible, and that handles them gracefully and optionally logs relevant information for when they occur.

The following section deals with detecting and handling errors, or exceptions in .NET parlance; later in this chapter, you learn how to log errors and shield your users from ugly pages with detailed exception messages.

# # Catching and Handling Exceptions

Normally, when serious exceptions occur, the user is presented with an error message. For example, if you try to send a message to a mail server that is not up and running, or doesn't allow you to connect to it, you'll get an exception that provides details about the error. The exception that you get is an instance of a class that inherits the System. Exception class, the base class for all exceptions. Many exceptions exist, each serving a distinct purpose.

By default, this exception bubbles all the way to the user interface where it is presented as a so-called Yellow Screen of Death, a reference to Windows "Blue Screen of Death" that you get when Windows crashes. You see a real example of this error in the next exercise.

Obviously, it is a lot better if you can anticipate the exception and write some code that prevents it from appearing in the user interface. You, for example, display a nicely formatted message to users instead, informing them the message could not be sent at the moment.

Fortunately, for these scenarios is integrated deeply in the .NET programming languages such as C# and Visual Basic. In these languages, you can use Try Finally blocks (try finally in C#) where code that could potentially throw an exception is wrapped in a Try block. Note that the VB.NET and C# versions of these keywords only differ in case; I refer to the capitalized version in the remainder of the text, in code blocks.

When an exception occurs, the remainder of the code in the Try block is skipped and code in a Catch block can run to deal with the error. You can have multiple Catch blocks that all deal with specific exceptions, but only the first block catches the exception type will fire. Therefore, it's important to order the various Catch blocks from generic to specific in order to handle the exception in the most specific Catch block. You see more of this later.

A Try or catch block can be followed by a Finally block. Code in a Finally block is always executed, regardless of whether an exception occurred or not, and such is an ideal location for some clean-up code.

Both Catch and Finally blocks are optional, although you need at least one of them.

The code in the following example tries to send an e-mail and then sets the Property of a Label to the value of the userMessage. Note: myMessage and mySmtClient are created by code not shown in this example. The userMessage is assigned a value in either the Try block (when the code executed successfully) or in the Catch block (when an error occurred). Either way, this userMessage is always assigned to the Label in the Finally block: