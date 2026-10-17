The response is actually more interesting than it looks. The debugger not only prints the result but kindly assigns it to a local variable for you to use in future evaluations. In this example, the number 4 (the length of the scheme string) was assigned to the variable $1. To use this is simple. Imagine you can't work out in your head the math necessary to multiply the length by two. No problem! GDB can do it for you!

```
p (NSUInteger)($1 * 2)
```

GDB performs this complex computation and responds with:

```
$2 = 8
```

Notice how even that evaluation was assigned to a new variable, $2. There are many more tricks up print’s sleeves, which you can find at http://xcodebook.com /printf, but let’s move on.

# VIEWING THE BACKTRACE

The backtrace in the current (paused) point in the application is the same information that is displayed under a paused thread in the Debug navigator: the stack. While Xcode’s user interface gives you nicely formatted information that can be used to navigate and control the debugging session, it’s not very handy for sharing information with others on a forum or mailing list, for example. It’s often helpful to be able to obtain a textual representation of the backtrace. Assuming TestApp is still paused in the same place as in the previous examples, issuing a backtrace command (bt for short) produces the following output:

```
#0  -[TestAppAppDelegate applicationDidFinishLaunching:]
    → (self=0x10015e520, _cmd=0x7fff84ad29c5, aNotification=
    → 0x114029af0) at /Users/jnozzi/Path/To/TestApp Suite/TestApp/
    → TestApp/TestAppAppDelegate.m:42

#1  0x00007fff83b568ea in _nsnote_callback ()

#2  0x00007fff835f1000 in __CFXNotificationPost ()

#3  0x00007fff835dd578 in _CFXNotificationPostNotification ()
```