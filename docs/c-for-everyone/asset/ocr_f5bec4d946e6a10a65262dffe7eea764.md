> A recursive computation solves a problem by using the same problem with simpler inputs.

> For a recursion to terminate, there must be special cases for the simplest inputs.

```
}
cout << endl;
```

Look at the print_triangle function one more time and notice how utterly reasonable it is. If the side length is 0, nothing needs to be printed. The next part is just as reasonable. Print the smaller triangle and don't think about why that works. Then print a row of []. Clearly, the result is a triangle of the desired size.

There are two key requirements to assure that the recursion is successful:

+   - Every recursive call must simplify the task in some way.
+   - There must be special cases to handle the simplest tasks directly.

The print_triangle function calls itself again with smaller and smaller side lengths. Eventually the side length must reach 0, and the function stops calling itself.

Here is what happens when we print a triangle with side length 4.

+   - The call `printTriangle(4)` calls `printTriangle(3)`.
+     - The call `printTriangle(3)` calls `printTriangle(2)`.
+       - The call `printTriangle(2)` calls `printTriangle(1)`.
+         - The call `printTriangle(1)` calls `printTriangle(0)`.
+           - The call `printTriangle(0)` returns, doing nothing.
+         - The call `printTriangle(1)` prints `[]`.
+       - The call `printTriangle(2)` prints `[][]`.
+     - The call `printTriangle(3)` prints `[][][][]`.
+   - The call `printTriangle(4)` prints `[][][][][][]`.

The call pattern of a recursive function looks complicated, and the key to the successful design of a recursive function is *not to think about it*.

![](bbox=[0.275, 0.59, 0.504, 0.756])

> This set of Russian dolls looks similar to the call pattern of a recursive function.

```
**ch05/triangle.cpp**

```cpp
#include <iostream>

using namespace std;

/**
    Prints a triangle with a given side length.
    @param side_length the side length (number of [] along the base)
*/
```
```