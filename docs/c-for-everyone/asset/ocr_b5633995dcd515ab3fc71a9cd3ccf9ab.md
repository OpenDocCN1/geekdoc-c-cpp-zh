If you prefer, you can implement this function more compactly:

```
int triangle_area(int side_length)
{
    if (side_length == 1) { return 1; }
    else
    {
        return triangle_area(side_length - 1) + side_length;
    }
}
```

We will look at the longer, more explicit form in this section.
Here is a trace of the function call `triangle_area(4)`.

+   - The `triangle_area` function executes with the parameter variable `side_length` set to 4.
+   - It sets `smaller_side_length` to 3 and calls `triangle_area` with argument `smaller_side_length`.
+     - That function call has its own set of parameter and local variables. Its `side_length` parameter variable is 3, and it sets its `smaller_side_length` variable to 2.
+     - The `triangle_area` function is called again, now with argument 2.
+       - In that function call, `side_length` is 2 and `smaller_side_length` is 1.
+       - The `triangle_area` function is called with argument 1.
+         - That function call returns 1.
+       - The function call sets `smaller_area` to 1 and returns `smaller_area + side_length = 1 + 2 = 3`.
+     - The function call sets `smaller_area` to 3 and returns `smaller_area + side_length = 3 + 3 = 6`.
+   - The function call sets `smaller_area` to 6 and returns `smaller_area + side_length = 6 + 4 = 10`.

> A recursive computation solves a problem by using the solution to the same problem with simpler inputs.

As you can see, the function calls itself multiple times, with ever simpler arguments, until a very simple case is reached. Then the recursive function calls return, one by one.

While it is good to understand this pattern of recursive calls, most people don’t find it very helpful to think about the call pattern when designing or understanding a recursive solution. Instead, look at the `triangle_area` function one more time. The first part is very easy to understand. If the side length is 1, then of course the area is 1. The next part is just as reasonable. Compute the area of the smaller triangle. Don’t worry how that works—treat the function as a black box and simply assume that you will get the correct answer. Then the area of the larger triangle is clearly the sum of the smaller area and the side length.

When a function keeps calling itself, you may wonder how you know that the calls will eventually come to an end. Two conditions need to be fulfilled:

+   - Every recursive call must simplify the computation in some way.
+   - There must be special cases to handle the simplest computations directly.

> For a recursion to terminate, there must be special cases for the simplest inputs.

The `triangle_area` function calls itself with a smaller side length. Eventually the side length must reach 1, and there is a special case for computing the area of a triangle with side length 1. Thus, the `triangle_area` function always succeeds.