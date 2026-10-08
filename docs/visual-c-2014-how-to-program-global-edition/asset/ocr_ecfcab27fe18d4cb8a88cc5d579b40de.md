# 7.11 Method-Call Stack and Activation Records 305

app declares two other methods—UseLocalVariable (lines 34–43) and UseStatistic(lines 46–53)—that take no arguments and do not return results. Method Main calls each method twice (lines 19–28). Method LocalVariable declares local variable x (line 36). WhenLocalVariable is first called (it creates local variable x and initializes it to 25 (line 36), outputs the value of x (lines 38–39), increments x (line 40) and outputs the value of x again (lines 41–42). WhenLocalVariable is called a second time (line 25), it re-creates local variable x and reinitializes it to 25, the output of each call to LocalVariable is identical.

Method StatisticVariable does not declare any local variables. Therefore, when it refers to x, static x (line 8) of the class is used. When StatisticVariable is first called (line 22), it outputs the value (1) of static x (lines 48–49), multiplies the static variable by 10 (line 50) and outputs the value (10) of static variable x again (lines 51–52) before returning. The next time StatisticVariable is called (line 28), the static variable has its modified value, 10, so it outputs 100. Finally, in Main, the app outputs the value of local variable x again (line 30) to show that none of the method calls modified Main's local variable x, because the methods referred to variables named x in other scopes.

# 7.11 Method-Call Stack and Activation Records

To understand how C performs method calls, we first need to consider a data structure (i.e., collection of related data items) known as a stack. Think of a stack as a pile of dishes. When a dish is placed on the pile, it is placed at the top—pushing the dish onto the stack. Similarly, when a dish is removed from the pile, it is popped off. Stacks are last-in-first-out (LIFO) data structures—the last item pushed (inserted) on the stack is the first item popped (removed) from the stack.

# 7.11.1 Method-Call Stack

One of the most important mechanisms for computer science students to understand is the method-call stack (sometimes referred to as the program-execution stack). This data structure—“behind the scenes”—supports the method call/return mechanism. It also supports the creation, maintenance and destruction of each method's local variables. As we see in Figs. 7.11–7.13, last-in-first-out (LIFO) is exactly what a method needs in order to return control to the method that called.

# 7.11.2 Stack Frames

As each method is called, it may, in turn, call all other methods,which—before any of the methods return—each method eventually must return control to the method that it called. So, however, the system must keep track of the return addresses that each method needs in order to return control to the method it called. The method-call stack is the perfect data structure for handling this information. Each time a method is called, an entry is pushed onto the stack. This entry, called stack frame or an activation record, contains the return address that the called method needs in order to return the calling method. It also contains some additional information. If the called method returns instead of calling another method-