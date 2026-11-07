+   c. Advance `first` to point to the next node.
+   d. Make `trail` point to the node before `current`.
+   e. Make `p` point to an empty list.
+   f. Set the value of the node before `last` to `54`.
+   g. Write a `while` loop to make `first` point to the node with `info` `5`.

10. Mark each of the following statements as valid or invalid. If a statement is invalid, explain why. (3, 4)

+   a. `p = list->link;`
+   b. `first = list;`
+   c. `temp->link = nullptr;`
+   d. `current->link = temp->info;`
+   e. `p = *last;`
+   f. `first = 90;`
+   g. `p->link->info = current->info;`
+   h. `current->info = temp->link;`
+   i. `*list = *temp;`
+   j. `temp->link = last->link->link;`
+   k. `cout << trail->link->link->info;`

11. Write C++ statements to do the following. (3, 4)

+   a. Write a C++ code so that `first` traverses the entire list.
+   b. Create the node with `info` `17` and insert after `current`.
+   c. Delete the last node of the list and also deallocate the memory occupied by this node. After deleting the node make `last` point to the last node of the list and the link of the last node must be `nullptr`.
+   d. Delete the node with `info` `92`. Also, deallocate the memory occupied by this node.
+   e. Write a C++ code to move the node with `info` `46` after `current` by adjusting the links of nodes in the linked list.

12. What is the output of the following C++ code? (3, 4)

```
while (first != last)
{
    cout << first->info << " ";
    first = first->link;
}
cout << last->info << endl;
```