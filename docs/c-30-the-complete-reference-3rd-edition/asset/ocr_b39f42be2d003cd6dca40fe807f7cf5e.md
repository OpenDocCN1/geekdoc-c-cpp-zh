The output is shown here. Pay special attention to the summation value.

```
0
1
2
3
Summation of 3 is 6
```

```
0
1
2
3
4
5
Summation of 5 is 21
```

As you can see, the count still proceeds normally. However, notice the summation value for 5. It shows 21 instead of 15! The reason for this is that sum is captured by ctObj when it is created by the Counter() method. This means it remains in existence until count is subject to garbage collection at the end of the program. Thus, its value is not destroyed when Counter() returns or with each call to the anonymous method when count is called in Main().

Although captured variables can result in rather counterintuitive situations, such as the one just shown, it makes sense if you think about it a bit. The key point is that when an anonymous method captures a variable, that variable cannot go out of existence until the delegate that captures it is no longer being used. If this were not the case, then the captured variable could be undefined when it is needed by the delegate.

# Lambda Expressions

Although anonymous methods are a valuable feature, they have been largely superceded by a better approach: the lambda expression. It is not an overstatement to say that the lambda expression is one of the two most important features added by C# 3.0 (the other being LINQ). Based on an entirely new syntactic element, the lambda expression provides a powerful alternative to the anonymous method. Although a principal use of lambda expressions is found when working with LINQ (see Chapter 19), they are also applicable to (and commonly used with) delegates and events. This use of lambda expressions is described here.

A lambda expression is the second way that an anonymous function can be created. (The other type of anonymous function is the anonymous method, described in the preceding section.) Thus, a lambda expression can be assigned to a delegate. Because a lambda expression is more streamlined than the equivalent anonymous method, lambda expressions are now the recommended approach in almost all cases.

# The Lambda Operator

All lambda expressions use the new lambda operator, which is =>. This operator divides a lambda expression into two parts. On the left is the input parameter (or parameters) is specified. On the right is the lambda body. The => operator is sometimes verbalized as "goes to" or "becomes."