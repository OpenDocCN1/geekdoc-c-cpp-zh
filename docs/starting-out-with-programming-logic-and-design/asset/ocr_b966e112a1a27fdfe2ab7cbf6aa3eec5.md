# 5.3 Count-Controlled Loops and the For Statement

In the flowchart, assume counter is an Integer variable. The first step is to set a counter to the appropriate starting value. Then, determine whether counter is less than or equal to the maximum value. If this is true, the body of the loop executes. Otherwise, notice that in the body of the loop one or more statements are executed, and 1 is added to counter.

For example, look at the flowchart in Figure 5-13. First, an Integer named counter is declared and initialized with the starting value 1. Then, the expression counter <= 5 is tested. If this expression is true the message "Hello world" is displayed and 1 is added to counter. Otherwise, the program exits the loop. If you follow the logic of this program you will see that the loop will iterate five times.

Figure 5-13 A count-controlled loop

![](bbox=[0.293, 0.32335, 0.663, 0.731])

# The For Statement

Count-controlled loops are so common in programming that most languages provide a statement just for them. This is usually called the For statement. The For statement is specifically designed to initialize, test, and increment a counter variable. Here is the general format that we will use to write the For statement in pseudocode: