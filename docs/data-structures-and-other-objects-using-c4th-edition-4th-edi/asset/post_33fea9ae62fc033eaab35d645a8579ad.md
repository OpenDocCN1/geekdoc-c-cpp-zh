
![](img/7bf56f684fab50d5ff9e94ae2818f3ac_303_0.png)

Notice that cursor and precursor are pointers to nodes rather than actual nodes.

Start your implementation by writing the header file and the invariant for the new sequence class. You might even write the invariant in large letters on a sheet of paper and pin it up in front of you as you work. Each of the member functions counts on that invariant being true when the function begins. And each function is responsible for ensuring that the invariant is true when the function finishes.

Keep in mind the four rules for a class that uses dynamic memory:

- 1. Some of your member variables are pointers. In fact, for your sequence class, four member variables are pointers.
- 2. Member functions allocate and release memory as needed. Don't forget to write documentation indicating which member functions allocate dynamic memory so that experienced programmers can deal with failures.
- 3. You must override the automatic copy constructor and the automatic assignment operator. Otherwise two different sequences end up with pointers to the same linked list. Some hints on these implementations are given in the following “value semantics” section.
- 4. The class requires a destructor, which is responsible for returning all dynamic memory to the heap.

## The Revised Sequence Class—Value Semantics

The value semantics of your new sequence class consists of a copy constructor and an assignment operator. The primary job of both these functions is to make one sequence equal to a new copy of another. The sequence that you are copying is called the “source,” and we suggest that you handle the copying in these cases:

- 1. If the source sequence has no current item, then simply copy the source’s linked list with list_copy. Then set both precursor and cursor to the null pointer.
- 2. If the current item of the source sequence is its first item, then copy the source’s linked list with list_copy. Then set precursor to null, and set cursor to point to the head node of the newly created linked list.

what is the invariant of the new sequence class?

- 3. If the current item of the source sequence is after its first item, then copy the source’s linked list in two pieces using `list_piece` from Self-Test Exercise 24 on page 258. The first piece that you copy goes from the head pointer to the precursor; the second piece goes from the cursor to the tail pointer. Put these two pieces together by making the link field of the precursor node point to the cursor node. The reason for copying in two separate pieces is to easily set the precursor and cursor.

After copying the linked list, be sure to set `many_nodes` to equal the number of nodes in the source. Also, beware of the potential pitfalls that accompany the implementation of your assignment operator (see “The Assignment Operator Causes Trouble with Linked Lists” on page 265).

To test the new sequence class, you can use the same interactive test program that you used to test your original sequence (see “Interactive Test Programs” on page 133).

## Self-Test Exercises for Section 5.4

- 36. Why is a precursor node pointer necessary in the linked-list implementation of a sequence class?
- 37. Suppose a sequence contains your three favorite strings, and the current item is the first item in the sequence. Draw the member variables of this sequence using our suggested implementation.
- 38. Write a new member function to remove a specified item from a sequence. The function has one parameter (the item to remove). After the removal, the current item is the item after the removed item (if there is one). You may assume that `value_after` has `==` and `!=` operators defined.
- 39. Which of the sequence member functions allocate dynamic memory?
- 40. Which of the sequence functions might use `list_piece` from Self-Test Exercise 24?

## 5.5 DYNAMIC ARRAYS VS. LINKED LISTS VS. DOUBLY LINKED LISTS

Many classes can be implemented with either dynamic arrays or linked lists. Certainly the bag, the string, and the sequence classes could each be implemented with either approach.

Which approach is better?

There is no absolute answer. But there are certain operations that are better performed by dynamic arrays and others where linked lists are preferable. Here are some guidelines:

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

![](img/7bf56f684fab50d5ff9e94ae2818f3ac_305_0.png)

FIGURE 5.15 Doubly Linked List

Resizing can be inefficient for a dynamic array. A container class that uses a dynamic array generally provides a resize function to allow a programmer to adjust the capacity as needed. But resizing an array can be inefficient. The new memory must be allocated, the items are then copied from the old memory to the new memory, and then the old memory is deleted. If a program can predict the necessary capacity ahead of time, then resizing is not a big problem, since the object can be given sufficient capacity from the outset. But sometimes the eventual capacity is unknown and a program must continually adjust the capacity. In this situation, a linked list has advantages. When a linked list grows, it grows one node at a time, and there is no need to copy items from old memory to new larger memory.

If a class is frequently adjusting its size, then a linked list may be better than a dynamic array.

## Making the Decision

Your decision on what kind of implementation to use is based on your knowledge of which operations occur in the class, which operations you expect to be performed most often, and whether you expect your containers to require frequent resizing. Figure 5.16 summarizes these considerations.

## Self-Test Exercises for Section 5.5

- 41. What underlying data structure is quickest for random access?
- 42. What underlying data structure is quickest for insertions/deletions at a cursor?
- 43. What underlying data structure is best if a cursor must move both forward and backward?
- 44. What is the typical worst-case time analysis for a resizing operation on a container class that is implemented with a dynamic array?
- 45. Implement a complete class for nodes of a doubly linked list. All member functions should be inline functions.
- 46. For your dnode class in the previous exercise, write a function that adds a new item at the head of a doubly linked list.

FIGURE 5.16 Guidelines for Choosing Between a Dynamic Array and a Linked List

| Frequent random access operations | Use a dynamic array |
| --- | --- |
| Operations occur at a cursor | Use a linked list |
| Operations occur at a two-way cursor | Use a doubly linked list |
| Frequent resizing may be needed | A linked list avoids resizing inefficiency |
