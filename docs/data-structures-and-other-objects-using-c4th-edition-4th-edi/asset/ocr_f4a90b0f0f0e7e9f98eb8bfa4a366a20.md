# Reference Type as a Return Value

A function can use a reference type as a return value by placing the symbol & after the return type name. The use of a reference type has these effects:

+   1. The return value must be a variable or object that will still exist after the function returns. In particular, the return value must not be a local variable.
+   2. The function returns this actual variable or object (not a copy of the object).

Let's look at an example to see how the new data function can be used to change the data field of a node. Suppose that cursor is pointing to the second node of this linked list of strings:

![](bbox=[0.18, 0.415, 0.7, 0.495])

Let's examine some statements to see how cursor->data() can be used to directly manipulate the data field of the second node:

```
cursor->data() = "myrie";
```

This is simply an assignment statement, but the left side of the assignment is a reference to the actual data field of the cursor's node, so this data will change to the string "myrie", as shown here:

![](bbox=[0.18, 0.635, 0.7, 0.705])

An assignment to a node's data field is not too exciting; we could have accomplished the same thing with cursor->set_data("myrie"). A better example shows how we can change a node's data by activating one of its member functions. For example, consider this statement for the preceding linked list:

```
head_ptr->data().erase(0,2);
```

The string's erase(0,2) member function erases two characters starting at the front of the string, changing "eenie" to "nie" and resulting in the linked list shown here: