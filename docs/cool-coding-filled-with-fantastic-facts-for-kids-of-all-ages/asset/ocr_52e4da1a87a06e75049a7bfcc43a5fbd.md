Programmers refer to these as 'bad smells' - they are signs that the code may work, but it will be difficult to change without accidentally breaking something, and when it breaks it will be hard to fix.

Don't worry if your code has one or more of the above; programs that change over time often end up like this. The solution is refactoring,

which is like spring-cleaning for code. It's the process of changing the code, not to make it do new things, but to be more manageable while doing the same thing. This usually involves turning duplicated code into a single function that can be called from multiple places, breaking up overlong lines and functions into separate chunks, and replacing goto statements with functions and loops.

![](bbox=[0.0, 0.34, 0.26, 0.95])

![](bbox=[0.33, 0.5, 0.73, 0.96])

![](bbox=[0.78, 0.15, 1.0, 0.76])