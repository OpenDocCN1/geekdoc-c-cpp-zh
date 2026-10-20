sive, because at that point the calls are initiated by method fibonacci itself. Each time fibonacci is called, it immediately tests for the base cases—number equal to 0 or number equal to 1 (Fig. 18.5, lines 12–13). We use BigInteger constants ZERO and ONE to represent the values 0 and 1, respectively. If the condition in lines 12–13 is true, fibonacci simply returns number, because fibonacci(0) is 0 and fibonacci(1) is 1. Interestingly, if number is greater than 1, the recursion step generates two recursive calls (lines 16–17), each for a slightly smaller problem than the original call to fibonacci. Lines 16–17 use BigInteger methods add and subtract to help implement the recursive step. We also use a constant of type BigInteger named TWO that we defined at line 7.

# Analyzing the Calls to Method Fibonacci

Figure 18.6 shows how method fibonacci evaluates fibonacci(3). At the bottom of the figure we’re left with the values 1, 0 and 1—the results of evaluating the base cases. The first two return values (from left to right), 1 and 0, are returned as the values for the calls fibonacci(1) and fibonacci(0). The sum 1 plus 0 is returned as the value of fibonacci(2). This is added to the result (1) of the call to fibonacci(1), producing the value 2. This final value is then returned as the value of fibonacci(3).

![](bbox=[0.12, 0.55, 0.88, 0.75])

Fig. 18.6 | Set of recursive calls for fibonacci(3).

Figure 18.6 raises some interesting issues about the order in which Java compilers evaluate the operands of operators. This order is different from that in which operators are applied to their operands—namely, the order dictated by the rules of operator precedence. From Figure 18.6, it appears that while fibonacci(3) is being evaluated, two recursive calls will be made—fibonacci(2) and fibonacci(1). But in what order will they be made? The Java language specifies that the order of evaluation of the operands is from left to right. Thus, the call fibonacci(2) is made first and the call fibonacci(1) second.

A word of caution is in order about recursive programs like the one we use here to generate Fibonacci numbers. Each invocation of the fibonacci method that does not match one of the base cases (0 or 1) results in two more recursive calls to the fibonacci method. Hence, this set of recursive calls rapidly gets out of hand. Calculating the Fibonacci value of