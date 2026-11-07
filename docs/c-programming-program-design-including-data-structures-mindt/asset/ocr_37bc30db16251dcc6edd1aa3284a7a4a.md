```
```cpp
current->info = 72;
current->link = nullptr;
trail = current;
current = new nodeType;
current->info = 46;
current->link = trail;
list = current;
current = new nodeType;
current->info = 52;
list->link = current;
current->link = trail;
trail = current;
current = new nodeType;
current->info = 91;
current->link = trail->link;
trail->link = current;
current = list;
while (current != nullptr)
{
    cout << current->info << " ";
    current = current->link;
}
cout << endl;
```
```

17. Assume that the node of a linked list is in the usual `info-link` form with the info of the type `int`. The following data, as described in parts (a) to (d), is to be inserted into an initially linked list: 72, 43, 8, 12. Suppose that head is a pointer of type `nodeType`. After the linked list is created, head should point to the first node of the list. Declare additional variables as you need them. Write the C++ code to create the linked list. After the linked list is created, write a code to print the list. What is the output of your code? (3, 4)

+   a. Insert 72 into an empty linked list.
+   
+   b. Insert 43 before 72.
+   
+   c. Insert 8 at the end of the list.
+   
+   d. Insert 12 after 43.

18. Assume that the node of a linked list is in the usual `info-link` form with the info of the type `int`. (`list` and `ptr` are pointers of type `nodeType`.) The following code creates a linked list. (3, 4)

```
```cpp
ptr = new nodeType;
ptr->info = 16;
list = new nodeType;
list->info = 25;
list->link = ptr;
ptr = new nodeType;
ptr->info = 12;
ptr->link = nullptr;
list->link->link = ptr;
```
```