
## 1.9 FLOWCHARTS

A very effective tool to show the logic flow of a program is the flowchart. A flowchart is a pictorial representation of an algorithm. It hides all the details of an algorithm by giving a picture; it shows how the algorithm flows from beginning to end. In a programming environment, it can be used to design a complete program or just a part of the program.

The primary purpose of a flowchart is to show the design of the algorithm. At the same time, it relieves the programmers from the syntax and details of a programming language while allowing them to concentrate on the details of the problem to be solved. This is in contrast to another programming design tool, the pseudocode, which provides a textual design solution. Both tools have their advantages, but a flowchart has the pictorial power that other tools lack. Figure 1.6 is a flowchart that describes the process of reading, adding, printing three numbers, and printing the result.

![](img/a99ec79093c067f0bed8f1086197950e_34_0.png)

**Fig. 1.6 Flowchart for adding three numbers**

## 1.10 ANALYSIS OF ALGORITHMS

Algorithms heavily depend on the organization of data. There can be several ways to organize data and/or write algorithms for a given problem. The difficulty lies in deciding which algorithm is the best. We can compare one algorithm with the other and choose the best. For comparison, we need to analyse the algorithms. Analysis involves measuring the performance of an algorithm. Performance is measured in terms of the following parameters:

- 1. *Programmer's time complexity*—Very rarely taken into account as it is to be paid for once
- 2. *Time complexity*—The amount of time taken by an algorithm to perform the intended task
- 3. *Space complexity*—The amount of memory needed to perform the task.

It is very convenient to classify algorithms on the basis of the relative amount of time and space they require and specify the growth of time and space requirements as a function of the input size.

### 1.10.1 Complexity of Algorithms

Algorithms are measured in terms of time and space complexity. The *time complexity* of an algorithm is a measure of how much time is required to execute an algorithm for a given number of inputs and is measured by its rate of growth relative to standard functions.

Space complexity is similar to time complexity. The space complexity of an algorithm is a measure of how much storage is required by the algorithm. It is possible to design an algorithm that uses more space and less time or less space and more time.

Typically, computer scientists are interested in minimizing the time complexity of algorithms. The economics of storage versus the speed of computers is the principal factor that determines the focus on time complexity. The cost of memory has decreased at an exponential rate over the past 25 years, whereas the cost of central processing unit time has not decreased at that rate. The bottleneck is the execution time. Hence, computer scientists focus on the execution time of algorithms.

An algorithm can be characterized by a timing function T(n). T(n) is a measure of how much time is required to execute an algorithm with the given n data values. For example, the timing function for a sort operation specifies the time required to sort n data values. The timing function for an algorithm that solves a system of linear equations specifies the time required to solve n linear equations.

An algorithm O(n^2), pronounced 'oh of n squared', indicates that its timing function will grow no faster than the square of the number of data values it processes. Let us learn more about these two measures of algorithms.

### 1.10.2 Space Complexity

Space complexity is the amount of computer memory required during program execution as a function of the input size. Space complexity measurement, which is the space requirement of an algorithm, can be performed at two different times:

- 1. Compile time
- 2. Run time

### Compile Time Space Complexity

Compile time space complexity is defined as the storage requirement of a program at compile time.

This storage requirement can be computed during compile time. The storage needed by the program at compile time can be determined by summing up the storage size of each variable using declaration statements. For example, the space complexity of a non-recursive function of calculating the factorial of number n depends on the number n itself.

Space complexity = Space needed at compile time

This includes memory requirement before execution starts.

### Run-time Space Complexity

If the program is recursive or uses dynamic variables or dynamic data structures, then there is a need to determine space complexity at run-time. In general, this dynamic storage size is dependent on some parameters used in a program. It is difficult to estimate memory requirement accurately, as it is also determined by the efficiency of compiler. Memory requirement is the summation of the program space, data space, and stack space.

**Program space** This is the memory occupied by the program itself.

**Data space** This is the memory occupied by data members such as constants and variables.

**Stack space** This is the stack memory needed to save the function's run-time environment while another function is called. This cannot be accurately estimated since it depends on the run-time call stack, which can depend on the program's data set. This memory space is crucially important for recursive functions.

### 1.10.3 Time Complexity

Time complexity T(P) is the time taken by a program P, that is, the sum of its compile and execution times. This is system-dependent. Another way to compute it is to count the number of algorithm steps. An algorithm step is a syntactically or semantically meaningful segment of a program. We can determine the number of steps needed by a program to solve a particular problem instance in one of the following two ways:

- 1. Introduce a new variable, `count`, into the program. This is a global variable with initial value 0. Statements to increment count amount are introduced in the program at appropriate locations. This is done so that each time the statement in the original program is executed, the count is incremented by the step count of that statement. We measure the run-time of an algorithm by counting the number of steps.
- 2. Manually compute the number of times each statement will be executed. The number of times the statement is executed is its _frequency count_. Get the sum of frequency counts of all statements. This sum is the number of steps needed to solve a given problem.

### Best, Worst, and Average Cases

The best case complexity of an algorithm is the function defined by the minimum number of steps taken on any instance of size n.

The worst case complexity of an algorithm is the function defined by the maximum number of steps taken on any instance of size n.

The average case complexity of an algorithm is the function defined by an average number of steps taken on any instance of size n.

Each of these complexities defines a numerical function—time versus size.

### 1.10.4 Computing Time Complexity of an Algorithm

The total time taken by the algorithm or program is calculated using the sum of the time taken by each of the executable statements in an algorithm or a program. The time required by each statement depends on the following:

- 1. the time required for executing it once
- 2. the number of times the statement is executed

The product of these two parameters gives the time required for that particular statement. Compute the execution time of all executable statements. The summation of all the execution times is the total time required for that algorithm or program.

In general, when we sum up the frequency count of all the statements, we get a polynomial. In an analysis, we are interested in the order of magnitude of an algorithm, that is, we are interested in only those statements that have the greatest frequency count.

### 1.10.5 Big-O Notation

Given the speed of computers today, we are not concerned as much with the exact measurement of an algorithm's efficiency as we are with its general order of magnitude. If the analysis of two algorithms shows that one executes 15 iterations while the other executes 25 iterations, then they are both so fast that we cannot see the difference. On the other hand, if one iterates 15 times and the other iterates 1500 times, we should be concerned.

We have shown that the number of statements executed in the function for n elements of data is a function of the number of elements, expressed as f(n). Although the equation derived for a function may be complex, a dominant factor in the equation usually determines the order of magnitude of the result. Therefore, we do not need to determine the complex measure of efficiency but only the factor that determines the magnitude. This factor is the big-O, as in 'on the order of', and expressed as O(n), that is, on the order of n.

The simplification of efficiency is known as the big-O analysis. For example, if an algorithm is quadratic, we would say its efficiency is O(n^2) or on the order of n squared.

The big-O notation can be derived from f(n) using the following steps:

- 1. In each term, set the coefficient of the term to 1.
- 2. Keep the largest term in the function and discard the others. The terms are ranked from the lowest to the highest as follows:

```
log n ... n ... n log n ... n^2 ... n^3 ... n^k ... 2^n ... n!
```

For example,

- 1. To calculate the big-O notation for

```
f(n) = n x ((n + 1) / 2) = 1/2 n^2 + 1/2 n
```

we first remove all coefficients. This gives us

```
n^2 + n
```

which, after removing the smaller factors, gives us n^2
