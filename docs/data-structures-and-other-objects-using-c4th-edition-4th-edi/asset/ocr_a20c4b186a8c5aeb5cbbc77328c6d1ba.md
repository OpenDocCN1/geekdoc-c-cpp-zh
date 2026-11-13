After adding a fourth item, the list would look like this:

![](bbox=[0.26, 0.18, 0.81, 0.28])

The item for the new fourth entry is placed in a newly created node at the end of the list. Normally, this is accomplished by a function call and an assignment:

```
list_insert(rear_ptr, entry);
rear_ptr = rear_ptr->link();
```

To add the first item, we need a slightly different approach because the empty list has no rear pointer. In this case we should add the new entry at the head of the list, and then assign rear_ptr to also point to the new node, as shown in this segment of code:

```
if (empty()) {
    // Insert first entry.
    main_savitch_GB::list_head_insert(front_ptr, entry);
    rear_ptr = front_ptr;
}
else
{
    // Insert an entry that is not the first.
    main_savitch_GB::list_insert(rear_ptr, entry);
    rear_ptr = rear_ptr->link();
}
```

In fact, this code is most of the insert function. The only other work is to add one to the count member variable.

**The queue pop member function.** The pop operation removes a node from the front of the queue. For example, suppose we start with this queue:

![](bbox=[0.26, 0.685, 0.81, 0.77])

In this example, the pop function will remove the item that is labeled “Item A.” When pop returns, the list will have only three items, shown here: