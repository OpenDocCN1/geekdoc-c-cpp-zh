this, you can figure out which execution path your code followed until it ran into trouble!

Note that the stack trace includes calls from the .Net system; you don't normally need to follow all Microsofts System.Windows.Forms code to find out what went wrong, only the code that belongs to your own application.

So, why is this called a "stack trace"?

Because, every time a program calls a method, it keeps track of where it was. It has a data structure called the "stack", where it dumps its last location.

If it is done executing the method, it looks on the stack to see where it was before it called the method - and continues from there.

So the stack lets the computer know where it left off, before calling a new method.

But it also serves as a debugging help. Like a detective tracing the steps that a criminal took when committing their crime, a programmer can use the stack to trace the steps a program took before it crashed.