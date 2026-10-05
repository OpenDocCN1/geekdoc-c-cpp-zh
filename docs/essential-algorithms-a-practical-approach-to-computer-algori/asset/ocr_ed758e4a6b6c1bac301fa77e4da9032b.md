4. If an algorithm performs an operation that takes O(f(N)) steps, and for every step in that it performs another O(g(N)) steps, the algorithm's total performance is O(f(N) × g(N)).

5. Ignore constant multiples. If C is a constant, O(C × f(N)) is the same as O(f(N)), and O(f(C × N)) is the same as O(f(N)).

These rules may seem a bit formal, with all the f(N) and g(N), but they're fairly easy to apply. If they seem confusing, a few examples should make them easier to understand.

# Rule 1

If an algorithm performs a certain sequence of steps f(N) times for a mathematical function f, it takes O(f(N)) steps.

Consider the following algorithm, written in pseudocode, for finding the largest integer in array:

```
Integer: FindLargest(Integer: array[])
Integer: largest = array[]
For i = 1 To <largest index>
If (array[i] > largest) Then largest = array[i]
Next i
Return largest
EndLargest
```

The FindLargest algorithm takes as a parameter an array of integers and returns an integer result. It starts by setting the variable largest equal to the first value in the array.

It loops through the remaining values in the array, comparing each to largest. If it finds a value that is larger than largest, the program sets largest to that value.

After it finishes the loop, the algorithm returns largest. This algorithm examines each of the N items in the array once, so it has O(N) performance.

> NOTE Often algorithms spend most of their time in loops. There's no way an algorithm can execute more than N steps with a fixed number of code lines unless it contains some sort of loop.
Study an algorithm's loops to figure out how much time it takes.

# Rule 2

If an algorithm performs an operation that takes O(f(N)) steps and then performs a second operation that takes O(g(N)) steps for functions f and g, the algorithm's total performance is O(f(N) + g(N)).

If you look again at the FindLargest algorithm shown in the preceding section, you'll see that a few steps are not actually inside the loop. The following