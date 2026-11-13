5.
[3 2]
[0] [1]
We don't care what appears beyond data[1].

6. 0

7. Static member constants that are integer types can be given a value in the header file because integral values are often used within the class definition to define other objects, such as the size of an array.

8. See the two rules on page 110.

9. A short-circuit evaluation of a boolean expression evaluates the expression from left to right, stopping as soon as there is enough information to determine the value of the expression. If two logical operations in an expression must be true for the entire expression to be true, the second operation is not evaluated if the first operation is false.

10. copy(x, x+6, y+42);

11. It does not need to be a friend function because it does not directly access any private members of the bag.

```
```cpp
bag::size_type
bag::erase(const value_type& target)
{
    size_type index = 0;
    size_type many_removed = 0;

    while (index < used)
    {
        if (data[index] == target)
        {
            --used;
            data[index] = data[used];
            ++many_removed;
        }
        else
            ++index;
    }

    return many_removed;
}
```
```

13. The two statements can be replaced by one statement: data[index] = data[--used];

When --used appears as an expression, the variable used is decremented by one, and the resulting value is the value of the expression. (On the other hand, if used-- appears as an expression, the value of the expression is the value of used prior to subtracting one.) Similarly, the last two statements of insert can be combined to data[used++] = entry;. In this case, we have the expression used++ as the index because we want to use the old value of used (before adding one) as the index.

14. If we activate b = b, then the private member variable used is the same variable as addend.used. Each iteration of the loop adds 1 to used, and hence addend.used is also increasing, and the loop never ends. To correct the problem, you could store the initial value of addend.used in a local variable, and use this local variable to determine when the loop ends.

15. A running time of O(1) means that a function does not depend on the size of the input and runs in constant time.

16. Both contain a collection of items, but the items in a sequence are arranged in order, one after another. The start, advance, current, remove_current, attach, and is_item functions are required to manipulate items at a precise location.

17. Internal iterators use the member functions of a container to access the items of a container. External iterators have their own member functions to access items of a sequence.

```
```cpp
void sequence::insert
(const value_type& entry)
{
    size_type i;
    assert(size( ) < CAPACITY);

    if ( !is_item( ) )
        current_index = 0;
    for (i = used; i > current_index; --i)
        data[i] = data[i-1];
    data[current_index] = entry;
    ++used;
}
```
```