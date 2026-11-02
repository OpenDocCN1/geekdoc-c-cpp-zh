```
first = copy;
}
else
{
    just_copied->next = copy;
}
if (next_to_copy == other.last)
{
    last = copy;
}
next_to_copy = next_to_copy->next;
just_copied = copy;
}
}
```

We make both of these helper functions private because they should never be called by a class user. The free function assumes that the freed object is never used again, and the copy function assumes that it is called on an uninitialized object.

# References

Since we are thinking about memory management, this is a good time to make a simple but useful improvement to the List class. In order to avoid copying string objects, we should use constant references for all object parameters. Simply change parameters such as

```
void push_back(string element);
Iterator erase(Iterator iter);
```

to

```
void push_back(const string& element)
Iterator erase(const Iterator& iter);
```

Remember to update the member function definitions as well.

What about return values? You cannot return a reference to a local variable. For example, it would be an error to change the return type of the begin member function from Iterator to Iterator&:

```
Iterator& List::begin()
{
    Iterator iter;
    iter.position = first;
    iter.container = this;
    return iter; // Error—cannot return a reference to a local variable
}
```

A reference is a pointer in disguise. Here, we would return a pointer to iter, an object that is being reclaimed as soon as the begin function exits.

However, there is one place where we can return a reference. The Iterator::get member function returns data in a node. The node is allocated on the free store, and it still exists after the get member function exits:

```
const string& Iterator::operator*() const
{
    return position->data;
}
```

# Nested Classes

In Section 14.2, the List class used two helper classes, Node and Iterator. Other data structures also use nodes and iterators. To avoid conflicts, we could rename these particular classes into ListNode and ListIterator. However, there is a more elegant approach. We can nest the Node and Iterator classes inside the List class. We will make the Node class private because users of the list