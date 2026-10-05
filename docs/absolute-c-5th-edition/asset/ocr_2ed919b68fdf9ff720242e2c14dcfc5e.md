# 602 CHAPTER 13 Recursion

13.9 Iterative Version of Binary Search (part 2 of 2)

```
}
else if (key < a[mid]) {
    last = mid - 1;
}
else if (key > a[mid]) {
    first = mid + 1;
}
}
```

![](bbox=[0.068, 0.35, 0.203, 0.368])

# Self-Test Exercises

+   17. Write a recursive function definition for the following function:
int squares(int n);
//Precondition: n >= 1
//Returns the sum of the squares of the numbers 1 through n.
nFor example, squares(3) returns 14 because 1² + 2² + 3² is 14.

# Chapter Summary

+   * If a problem can be reduced to smaller instances of the same problem, a recursive solution is likely to be easy to find and implement.
* A recursive algorithm for a function definition normally contains two kinds of cases: one or more cases that include at least one recursive call and one more stopping cases where the problem is solved without any recursion.
* Mutual recursion occurs when two or more functions call each other.
* When writing a recursive function definition, always check to see that the function will not produce infinite recursion.
* When you define a recursive function, use the three criteria in the subsection "Recursive Design Techniques" to check that the function is correct.
* When designing a recursive function to solve a task, it is often necessary to solve a more general problem than the given task. This may be required for allow proper calls, since the smaller problems may not be exactly the same problem as the given task. For example, in the binary search problem, the task was to search an entire array, and the recursive solution is an algorithm to search any portion of the array (either all of it or a part of it).