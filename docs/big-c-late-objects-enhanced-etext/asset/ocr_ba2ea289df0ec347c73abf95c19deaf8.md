```
return 0;
}
```

# Program Run

```
Enter the side length: 10
[]
[[]]
[[[]]]
[[[[]]]]
[[[[[]]]]]
[[[[[[]]]]]]
[[[[[[[]]]]]]]
[[[[[[[[]]]]]]]]
[[[[[[[[[]]]]]]]]]
[[[[[[[[[[]]]]]]]]]]
[[[[[[[[[[[]]]]]]]]]]]
```

Recursion is not really necessary to print triangle shapes. You can use nested loops, like this:

```
for (int i = 0; i < side_length; i++)
{
    for (int j = 0; j < i; j++)
    {
        cout << "[ ]";
    }
    cout << endl;
}
```

However, this pair of loops is a bit tricky. Many people find the recursive solution simpler to understand.

![](bbox=[0.15, 0.83, 0.25, 0.97])

# HOW TO 5.2

# Thinking Recursively

To solve a problem recursively requires a different mindset than to solve it by programming loops. In fact, if it helps if you are, or pretend to be, a bit lazy and let others do most of the work for you. If you need to solve a complex problem, pretend that "someone else" will do most of the heavy lifting and solve the problem for all simpler inputs. Then you only need to figure out how you can turn the solutions with simpler inputs into a solution for the whole problem.

# Problem Statement

To illustrate the recursive thinking process, consider the problem of Section 4.2, computing the sum of the digits of a number. We want to design a function digit_sum that computes the sum of the digits of an integer n. For example, digit_sum(1729) = 1 + 7 + 2 + 9 = 19.

# Step 1

Break the input into parts that can themselves be inputs to the problem.

In your mind, fix a particular input or set of inputs for the task that you want to solve, and think how you can simplify the inputs. Look for simplifications that can be solved by the same task, and whose solutions are related to the original task.

In the digit sum problem, consider how we can simplify an input such as n = 1729. Would it help to subtract 1? After all, digit_sum(1729) = digit_sum(1728) + 1. But consider n = 1000. There seems to be no obvious relationship between digit_sum(1000) and digit_sum(999).

A much more promising idea is to remove the last digit, that is, compute n / 10 = 172. The digit sum of 172 is directly related to the digit sum of 1729.

The key to finding a recursive solution is reducing the input to a simpler input for the same problem.