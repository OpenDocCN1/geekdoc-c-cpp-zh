```
void show(ranges::view auto arg);
```

This prevents the call to `show(vector{1,2,3})`. If you want to enforce this, convert the container with `all` to `show(views::all(vector{1,2,3}))` explicitly into a view.

Ranges as parameters are a complex topic. You can find more details in Chapter 25, Section 25.6, under the subheading Ranges as Parameters (and More).

Each of the containers 24.1.3 Operations associated with the operations must be able to perform. Over time, more or less established names have emerged for this. Let's take as an example one of the simplest abstract data types, the `stack`.

A stack (theoretically) hold an unlimited number of elements. These are added with `push()`. At the end where you add, you can remove the most recently added element with `pop()`. This can be done until the stack is empty again, which is checked with `empty()`.

As minimum operations, this is sufficient for a stack. You can request additional “luxury operations,” but the minimum set is provided with this.

Do you want to know how many elements a given stack contains—that is, you want to know `size()`? Then copy all elements with `pop()` and `push()` to another stack until the original is `empty()`, count them, and when you are done, stack everything back. This is certainly not a fast method, but feasible in principle. Whether you want to