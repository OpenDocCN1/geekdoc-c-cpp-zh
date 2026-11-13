Our days of easy contentment are done. The automatic assignment operator fails for the dynamic bag (or for any other class that uses dynamic memory).

Here is an example to show what goes wrong. Suppose we set up a bag called x with an initial capacity of 5, containing the integers 10, 20, and 30—then we copy the private member variables of x to another bag y. The result is that the two pointers, x.data and y.data, both point to the same dynamic array, like this:

![](bbox=[0.26, 0.27, 0.82, 0.4])

The problem with this arrangement is that a subsequent change to x's array will also change y's array. Normally, this is not what we want; after an assignment y = x, we do not want further changes to one object to directly affect the other.

Instead, when we assign y = x, we want y to have its own dynamic array, completely separate from x's dynamic array. Of course, the dynamic array of y will contain the same values as the x array, but these two arrays will not share the same dynamic memory. The desired situation after the assignment looks like this:

![](bbox=[0.26, 0.54, 0.82, 0.68])

To achieve this situation, we must provide our own assignment operator rather than relying on the automatic assignment operator. We can do this by overloading the assignment operator for the bag class, in roughly the same way that we have overloaded other operators for the bag. The operator will be overloaded as a bag member function with the prototype given here:

```
```cpp
void bag::operator = (const bag& source);
// Postcondition: The bag that activated this function has the same items
// and capacity as source.
```
```