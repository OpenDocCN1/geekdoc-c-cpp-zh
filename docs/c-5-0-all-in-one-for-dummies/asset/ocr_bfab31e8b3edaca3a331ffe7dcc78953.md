# Chapter 9: Some Exceptional Exceptions

# In This Chapter

+   ✔ Handling errors via return codes
+   ✔ Using the exception mechanism instead of return codes
+   ✔ Plotting your exception-handling strategy

We know it's difficult to accept, but occasionally a method doesn't do what it's supposed to do. (If you need to learn about methods, read the first chapter of Book II). Even the ones we write — especially the ones we write — don't always do what they're supposed to. Users are notoriously unreliable as well. No sooner do you ask for an `int` than a user inputs a `double`. Sometimes, the method goes merrily along, blissfully ignorant that it is spewing out garbage. However, good programmers write their methods to anticipate problems and report them as they occur.

![](bbox=[0.12, 0.54, 0.22, 0.68])

I'm talking about runtime errors, not compile-time errors, which C# spits out when you try to build your program. Runtime errors occur when the program is running, not at compile time.

The C# exception mechanism is a means for reporting these errors in a way that the calling method can best understand and use to handle the problem. This mechanism has a lot of advantages over the ways that programmers handled errors in the, uh, good old days.

This chapter walks you through the fundamentals of exception handling. You have a lot to digest here, so lean back in your old, beat-up recliner.

# Using an Exceptional Error-Reporting Mechanism

C# introduces a completely different mechanism for capturing and handling errors: the exception. This mechanism is based on the keywords `try`, `catch`, `throw`, and `finally`. In outline form, it works like this: A method will try to execute a piece of code. If the code detects a problem, it will throw an error indication, which your code can catch, and no matter what happens, it finally executes a special block of code at the end, as shown in this snippet: