# Nodes and Linked Lists

operator, *, and without the parentheses, the dot operation would be performed first
(which would produce an error). The next paragraph describes a shortcut notation that
c avoid this worry about parentheses.

C++ has an operator that can be used with a pointer to simplify the notation for
sifying the members of a struct or a class. Chapter 10 introduced the arrow
operator., but we have not used it extensively before. So, a review is in order.
The arrow operator combines the actions of a dereferencing operator, *, and a dot
operator to specify a member of a dynamic struct or object that is pointed to
by a given pointer. For example, the previous assignment statement for changing the
first node can be written more simply

-> operator

```
head->count = 12;
```

This assignment statement and the previous one mean the same thing, but this one is
t form normally used.
The string in the first node can be changed from "rolls" to "bagels" with the
following statement:

```
head->item = "bagels";
```

The result of these changes to the first node in the list is diagrammed in Display 17.2.

# Display 17.2 Accessing Node Data

```
head->count = 12;
head->item = "bagels";
```

![](bbox=[0.139, 0.579, 0.86, 0.903])