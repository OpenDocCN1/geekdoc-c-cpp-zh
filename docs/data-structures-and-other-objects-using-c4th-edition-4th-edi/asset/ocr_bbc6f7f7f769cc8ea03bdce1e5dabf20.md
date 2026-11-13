Arrays are better at random access. The term random access refers to examining or changing an arbitrary element that is specified by its position in a list. For example: What is the 42nd item in the list? Or another example: Change the item at position 1066 to a 7. These are constant time operations for an array (or dynamic array). But, in a linked list, a search for item 1 must begin at the head and will take O(i) time. Sometimes there are ways to speed up the process, but even improvements remain in linear time.

If a class makes significant use of random access operations, then a dynamic array is better than a linked list.

Linked lists are better at insertions/deletions at a cursor. Our sequence class maintains a cursor that points to a “current element.” Typically, a cursor moves through a list one item at a time without jumping around to random locations. If all operations occur at the cursor, then a linked list is preferable to an array. In particular, insertions and deletions at a cursor are generally linear time for an array (since items that are after the cursor must all be shifted up or back to a new index in the array). But these operations are constant time operations for a linked list. Also remember that effective insertions and deletions in a linked list generally require maintaining both a cursor and a precursor (which points to the node before the cursor).

If class operations take place at a cursor, then a linked list is better than a dynamic array.

Doubly linked lists are better for a two-way cursor. Sometimes list operations require a cursor that can move forward and backward through a list—a kind of two-way cursor. This situation calls for a doubly linked list, which is like a simple linked list, except that each node contains two pointers: one pointing to the next node and one pointing to the previous node. An example of a doubly linked list of integers is shown in Figure 5.15. A possible set of definitions for a doubly linked list of items is the following:

```
class dnode
{
public:
typedef ---- value_type; <-- Fill in the value_type however you like.
...
private:
value_type data_field;
dnode *link_fore;
dnode *link_back;
};
```

The link_back field points to the previous node, and the link_fore points to the next node in the list.

If class operations take place at a two-way cursor, then a doubly linked list is the best implementation.

![](bbox=[0.12, 0.33, 0.22, 0.77])

FIGURE 5.15 Doubly Linked List