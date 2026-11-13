# 4.4.4 Linear Recursion

Depending on the way the recursion grows, it is classified as linear or tree. A recursive function is said to be linearly recursive when no pending operation involves another recursive call, for example, the Fact() function. This is the simplest form of recursion and occurs when an action has a simple repetitive structure consisting of some basic steps followed by the action again. The Factorial() function in Program Code 4.2 is an example of linear recursion.

# 4.4.5 Tree Recursion

In a recursive function, if there is another recursive call in the set of operations to be completed after the recursion is over, this is called a tree recursion. Examples of tree recursive functions are the quick sort and merge sort algorithms, the FibSeries algorithm, and so on.

The Fibonacci function FibSeries() is defined as

```
FibSeries(n) = 0, if n = 0
= 1, if n = 1
= FibSeries(n - 1) + FibSeries(n - 2), otherwise
```

Let n = 5.

```
FibSeries(0) = 0
FibSeries(1) = 1
FibSeries(2) = FibSeries(0) + FibSeries(1) = 1
FibSeries(3) = FibSeries(1) + FibSeries(2) = 2
FibSeries(4) = FibSeries(2) + FibSeries(3) = 3
FibSeries(5) = FibSeries(3) + FibSeries(4) = 5
```

Figure 4.1 demonstrates this explanation for n = 4.

![](bbox=[0.293, 0.663, 0.813, 0.853])

Fig. 4.1 Recursive calls in Fibonacci recursive function for n = 4