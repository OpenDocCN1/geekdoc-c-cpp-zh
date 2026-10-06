# Recursion That Returns Value 51

The factorial of a negative integer is undefined. You should have no trouble writing an iterative function based on this.

To define factorial(n) recursively, you first need to define factorial(n) in terms of factorial of a smaller number. To do so, observe that the factorial of n is equal to the factorial of (n - 1) multiplied by n; that is,

```
factorial(n) = n × [(n - 1) × (n - 2) × ... × 1]
n= n × factorial(n - 1)
```

The definition of factorial(n) in terms of factorial(n - 1), is an example of a recurrence relation. implies that you can also define factorial(n - 1) in terms of factorial(n - 2), and so on. This process is analogous to the dictionary search, in which you search a dictionary by searching a smaller dictionary in exactly the same way.

The definition of factorial(n) lacks one key element: the base case. As done in the dictionary search however, you must define one case differently from all the others, or else the recursion will never stop. The base case for factorial is factorial(0), which you know is 1. Because n decreases or factorial decrements by 1, you will always reach the base case. With the addition of the base case, the complete recursive definition of the factorial is

```
factorial(n) = {1 if n = 0\nn × factorial(n - 1) if n > 0
```

To be sure that you understand this recursive definition, apply it to the computation of factorial(4). Because 4>0, the recursive definition states

```
factorial(4) = 4 × factorial(3)
```

Similarly,

```
factorial(3) = 3 × factorial(2)
factorial(2) = 2 × factorial(1)
factorial(1) = 1 × factorial(0)
```

You have reached the base case, and the definition directly states

```
factorial(0) = 1
```

At this point, the application of the recursive definition stops and you still do not know the answer to the question: What is factorial(4)? However, the information to answer this question is available:

```
factorial(0) = 1, factorial(1) = 1 × 1 = 1
factorial(1) = 1, factorial(2) = 2 × 1 = 2
factorial(2) = 2, factorial(3) = 3 × 2 = 6
factorial(3) = 6, factorial(4) = 4 × 6 = 24
```

You can think of recursion as a process that divides a problem into a task that you can do and a task that a friend can do for you. For example if you compute factorial(4)

Your friend uses the same process to compute factorial(3) as you are using factorial(4). Your friend determines that factorial(3) is not the base case, and so asks another friend to compute factorial(2). Knowing factorial(2) enables your friend to compute factorial(3), and when you learn the value of factorial(3) from your friend, you can compute factorial(4).