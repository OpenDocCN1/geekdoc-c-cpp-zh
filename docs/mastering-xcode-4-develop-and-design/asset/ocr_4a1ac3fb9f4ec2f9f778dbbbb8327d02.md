# EXPLORING ANALYZER RESULTS

Following are a few examples of the types of issues the static analyzer can identify for you, with a walk-through of each result.

# MEMORY LEAKS

A simple description of a memory leak in a Cocoa application is an object to which you’ve lost any references and which thus can no longer be told to release its memory and go away. In this sense, the object’s memory is “leaked” as it cannot be reclaimed for the remainder of the application’s lifetime. Further, the object keeps living, which, depending on what the object does, can cause unexpected and sometimes very bad behavior.

Figure 17.2 showed an analyzer result for a memory leak. In this case, an NSString is leaked. From the top of the -init method, execution path is followed through the method. The issue is broken down into the two “steps” in the code that caused it.

In the first step, the instruction on line 16 returns an object with a +1 retain count (which, in a memory-managed environment, makes you responsible for properly releasing the object when necessary). In the second step, the method returns without releasing (or autoreleasing) the NSString instance beforehand. This means the NSString instance has been leaked at this point.

In the example, the fix is simple: Just uncomment line 19, where the string instance (assigned to message) is sent a -release (or you could send it an -autorelease).

NOTES: The code examples used are “quick and dirty” demonstrations and should not be used as examples of good coding practices for a number of reasons.

The memory management descriptions given here are oversimplified, but the particulars are beyond the scope of this book. For the purposes of this chapter, memory management issues refer to Objective-C objects in a manually memory-managed (versus garbage-collected) environment.

![](bbox=[0.0, 0.71, 0.26, 0.92])