operator, *, and so without the parentheses, the dot operation would be performed first (which would produce an error). The next paragraph describes a shortcut notation that can avoid this worry about parentheses.

C++ has an operator that can be used with a pointer to simplify the notation for specifying the members of a struct or a class. Chapter 10 introduced the arrow operator, ->, but we have not used it extensively before now. So, a review is in order. The arrow operator combines the actions of a dereferencing operator, *, and a dot operator to specify a member of a dynamic struct or class object that is pointed to by a given pointer. For example, the previous assignment statement for changing the number in the first node can be written more simply as

```
head->count = 12;
```

This assignment statement and the previous one mean the same thing, but this one is the form normally used.

The string in the first node can be changed from "rolls" to "bagels" with the following statement:

```
head->item = "bagels";
```

The result of these changes to the first node in the list is diagrammed in Display 17.2.

![](bbox=[0.134, 0.487, 0.862, 0.884])