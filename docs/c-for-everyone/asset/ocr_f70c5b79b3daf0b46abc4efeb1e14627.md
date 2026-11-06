Use the following recursive approach to check whether you can escape from the maze: If you are at an exit, return true. Recursively check whether you can escape from one of the empty neighboring locations without visiting the current location. This method merely tests whether there is a path out of the maze. Extra credit if you can print out a path that leads to an exit.

**P11.17** Extend the expression evaluator in Section 11.6 so that it can handle the % operator as well as a “raise to a power” operator ^. For example, 2 ^ 3 should evaluate to 8. As in mathematics, raising to a power should bind more strongly than multiplication: 5 * 2 ^ 3 is 40.

# ANSWERS TO SELF-CHECK QUESTIONS

+   1. Suppose we omit the statement. When computing the area of a triangle with `side_length 1`, we compute the area of the triangle with `side_length 0` as 0, and then add 1, to arrive at the correct area.

+   2. You would compute the smaller area recursively, then return `smaller_area + side_length + side_length - 1`.
+   
+   ```text
+   [][][][]
+   [][][][]
+   [][][][]
+   [][][][]
+   ```
+   
+   Of course, it would be simpler to compute the area simply as `side_length * side_length`. The results are identical because
+   
+   \[
+   1 + 0 + 2 + 1 + 3 + 2 + \cdots + n + n - 1 = \frac{n(n+1)}{2} + \frac{(n-1)n}{2} = n^2.
+   \]

+   3. There is no provision for stopping the recursion. When a number < 10 isn’t 8, then the function should return false and stop.

+   4.
+   
+   ```cpp
+   int pow2(int n)
+   {
+       if (n <= 0) { return 1; } // 2^0 is 1
+       else { return 2 * pow2(n - 1); }
+   }
+   ```

+   5.
+   
+   ```text
+   mystery(4) calls mystery(3)
+       mystery(3) calls mystery(2)
+           mystery(2) calls mystery(1)
+               mystery(1) calls mystery(0)
+                   mystery(0) returns 0.
+               mystery(1) returns 0 + 1 * 1 = 1
+           mystery(2) returns 1 + 2 * 2 = 5
+       mystery(3) returns 5 + 3 * 3 = 14
+   mystery(4) returns 14 + 4 * 4 = 30
+   ```

+   6. In this problem, *any* decomposition will work fine. We can remove the first or last character and then remove punctuation marks from the remainder. Or we can break the string in two substrings, and remove punctuation marks from each.