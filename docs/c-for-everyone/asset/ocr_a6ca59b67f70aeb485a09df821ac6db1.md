However, if the iterator is currently past the end, then you must make it point to the last element in the list.

```
void Iterator::previous()
{
    if (position == NULL)
    {
        position = container->last;
    }
    else
    {
        position = position->previous;
    }
}
```

The get function (which is the equivalent of the * operator) simply returns the data value of the node to which position points—that is, position->data. It is illegal to call get if the iterator points past the end of the list:

```
string Iterator::get() const
{
    return position->data;
}
```

Finally, the equals function (which is the equivalent of the == operator) compares two position pointers:

```
bool Iterator::equals(Iterator b) const
{
    return position == b.position;
}
```

![](bbox=[0.179, 0.542, 0.925, 0.885])

**Figure 4**  Advancing an Iterator