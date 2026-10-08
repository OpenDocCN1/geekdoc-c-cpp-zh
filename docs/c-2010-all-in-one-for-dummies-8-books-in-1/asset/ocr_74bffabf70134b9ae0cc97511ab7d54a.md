# 202 Planning Your Exception-Handling Strategy

Second, after you're safely past the IndexOf() call, one of the two method calls can throw an exception, even with line carefully checked out first. If spaceIndex turns out to be -1 (not found) — as can happen because the line that passes doesn't usually contain a namespace keyword — passing it to the first method can be a problem. You can guard for that, of course, like this:

```
if(spaceIndex > -1)
```

If spaceIndex is negative, the line doesn't contain the namespace keyword. That's not an error. You just skip that by returning the original line and then on to the next line. In any event, don't call the subordinate methods.

Method calls in your method require exploring each one to see which exceptions it can throw and digging into any methods that throw, and so on, until you reach the bottom of this particular call.

With this possibility in mind, and given that FixNamespaceLine() needs additional bulletproofing guard clauses first, where you might put an exception handler?

You might be tempted to put most of FixNamespaceLine() in a try block. But you have to consider whether this the best place for it. This method is low-level, so it should just throw exceptions as needed — or just pass on any exceptions that occur in the methods it calls. We recommend looking up the call to see which method would be a good location for a handler.

As you move up the call chain, ask the questions in the earlier section "Some questions to guide your planning.\ What would the consequences if FixNamespaceLine() threw an exception? That depends on how its result is used over the chain. Also, how wide does the need to be? If you "fix" the namespace line for the current file, does the user lose anything major? Maybe you can get away with an occasional unixed file, in which case you might choose to "swallow" the exception at some level in the call chain and just notify the user of the unprocessed file. Or maybe not. You get the idea. We discuss these and other exception-handling options in the article "Responding to an Exception" on csharp102.info.

The moral is correctly setting up exception handlers requires some analysis and thought.

However, keep in mind that any method can call throw exceptions — for example, the application could run out of memory, or the assembly's might not be found and loaded. You can't do much about that.

![](bbox=[0.139, 0.806, 0.233, 0.903])