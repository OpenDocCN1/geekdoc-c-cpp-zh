# Defining a Delegate

That callback method may be on the same class as the lengthy operation — such as phasing your sister on the other side of the house. Or, more often, it's on another class that knows about the progress bar — such as phasing Aunt Maxie in Minnesota. Somehow, at its start, the lengthy operation has been handed a mechanism for powering home — sort of giving your kid a cellphone so she can call you at 10 p.m.

This chapter talks about how your code can set up this callback mechanism and invoke it to phone home when needed.

Callbacks are used in Windows programming, typically for a piece of code, down in your program's guts, to notify a higher-level module that the task has finished, to ask for needed data, or to let module take a useful action, such as writing a log entry or update a progress bar.

![](bbox=[0.139, 0.296, 0.212, 0.366])

+   Figure 9-1: Making progress with the Windows ProgressBar control.

![](bbox=[0.25, 0.406, 0.638, 0.513])

# Defining a Delegate

C# provides delegates for making callbacks — and a number of other tasks. Delegates are the C# way (the .NET way, really, because any .NET language can use them) for you to pass around methods as though they were data.

You're saying, "Here, execute this method when you need it" — (and handing over the method to execute).

This chapter helps you get a handle on that concept, see its usefulness, and start using yourself.

You may be an experienced coder who will recognize immediately that delegates are similar to C/C++ function pointers — only much, much better. I'm assuming in this section that you aren't and don't.

Think of a delegate as a vehicle for passing a callback method to a "workhorse" method that needs to call you back or needs help with that action, as in doing the same action to each element of a collection. Because the