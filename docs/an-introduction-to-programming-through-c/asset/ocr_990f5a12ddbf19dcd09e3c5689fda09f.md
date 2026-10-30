# 12.5.1 Disabling assertions

Assertions are meant to be used in the debugging phase, when you are not completely sure about the correctness of your program. Once you become sure of the correctness of your, you may want to remove the assertions. This is because checking the assertions will take some time and will slow down the program. But it might be cumbersome to go through all the code and physically remove the assertions.

It turns out that is possible to disable assertions placed in your program without physically removing them. For this you put in the line

```
#define NDEBUG
```

at the top of each file containing assertions you want to disable. The above line is to be placed before the inclusion of <assert>. The above line will define the preprocessor (Appendix G) variable NDEBUG. This will have the effect of turning the assert statement into a comment.

# 12.6 Debugging

Suppose you follow the above directions and are generally very careful, and yet things go wrong: your program produces an answer different from what you expect. What do you do?

The most natural response is to try and find out when the program starts behaving differently from what you expect. For this, you can print out the values of the important variables at some convenient halfway point, and check if the values are as you might expect. If the values printed by these statements are as you expect (or not), then the error must be happening later (earlier), so you put print statements at later (earlier) points in your program. By examining the values in this manner, you try to get to a single statement until which the values are as you expect, but after which the values are different. At this point, you are usually in a position to determine what is going wrong. The process of examining the values taken by variables during execution can be made much easier if you use programs called debuggers or IDEs. We discuss them below.

We do note one important source of errors: it might be the case that your program is not working correctly not because it has a logical flaw, but because it is not being fed the correct data. This can happen especially if the input is coming from a badly designed input file which you have redirected. We discuss how to deal with this.

# 12.6.1 Debuggers and IDEs

There exist specialized programs, called debuggers or IDEs, Interactive Development Environments, which are modern versions of debuggers, which can substantially help in the process of debugging.

Debuggers or IDEs offer many ways of executing your program. For example, you can ask that the program be stepped, i.e. run one statement at a time. You can see where the control is after the execution of the statement in question ends, and you can also examine the values of the different variables. You can also ask that the program execute until a certain statement is reached, executing freely till that statement. Once that statement is