![](bbox=[0.34, 0.092, 0.823, 0.398])

| Statistics |  |
|---|---|
| Repetition | *n* |
| Testing | *n* + 1 |

The testing result should be the same in the last time false.

**Figure 5.10**  Analysis of a *while* statement

> > **A while statement is a pre-test loop.**  
> > If the body is executed *n* times,  
> > the condition has been tested (*n* + 1) times.

# 5.3 THE *for* STATEMENT

As we discussed in the previous section, we can always use the *while* statement as a counter-controlled loop. C++ provides another loop construct, however, called the *for* statement, that is particularly useful when we need counter-controlled iteration. It combines the three elements of a loop—initialization, conditional test, and update—into the loop construct itself. A quick comparison between the two loops shows that the *for* statement is much more compact than using a *while* statement for counter-controlled looping, as shown in Figure 5.11.

# 5.3.1 Header

We now discuss in detail each of the three sections in the header of a *for* statement.

![](bbox=[0.3, 0.747, 0.805, 0.892])

**Figure 5.11**  Comparison between a *while* loop and a *for* loop