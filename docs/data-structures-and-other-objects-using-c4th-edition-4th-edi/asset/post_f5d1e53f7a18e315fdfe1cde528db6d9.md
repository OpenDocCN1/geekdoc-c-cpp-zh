
- 9. The portions of the operating system that are currently in memory can be overwritten.

- 10. The implementation will compile correctly. But since the return value is a pointer to a node in the list, a programmer could use the return value to change the linked list. In general, the return value from a constant member function should never allow the underlying linked list to be changed.

- 11. Change the return type to const node*, and provide a second non-const function that returns the link as an ordinary node*.

- 12. We need only one function to access the data field because this function returns a copy of the data (and it is not possible to change the underlying linked list by having merely a copy of the data from a node).

- 13. The #include <string> directive must be added to the other include directives in the toolkit's header file. Then we can change the typedef statement to: typedef string value_type;

- 14. for (cursor = head_ptr; cursor != NULL; cursor = cursor->link()) {...}

- 15. A node pointer should be a value parameter when the function accesses and possibly modifies a linked list, but does not need to modify the pointer to point to a new node.

- 16. locate_ptr = locate_ptr->link(); If locate_ptr is already pointing to the last node before this assignment statement, then the assignment will set locate_ptr to the null pointer.

- 17. Using functions from Section 5.2:
```cpp
if (head_ptr == NULL)
    list_head_insert(head_ptr, 42);
else
    list_insert(head_ptr, 42);
```

- 18. if (head_ptr->link() == NULL)
    tail_ptr = head_ptr;

- 19. The new operator is used in the functions list_insert, list_copy, list_piece (if you implement it from Exercise 24), and list_head_insert. The delete operator is used in the functions list_head_remove, list_remove, and list_clear.

- 20. Never call delete unless you are actually reducing the number of nodes.

- 21. Using functions from Section 5.2:
```cpp
if (head_ptr == NULL)
{
    if (head_ptr->link() == NULL)
        list_head_remove(head_ptr);
    else
        list_remove(head_ptr);
}
```

- 22. It will be the null pointer.

- 23. The one line will be:
```cpp
previous_ptr->set_link(new node(entry, previous_ptr->link()));
```

- 24. The implementation is nearly the same as list_copy, but the copying must stop when the end node has been copied.

- 25. Here is the const version:
```cpp
const node*
const node* head_ptr,
size_t position
)
// size_t locations used: cassert, cstdlib
{
const node *cursor;
size_t i;
assert(0 <= position);
cursor = head_ptr;
for (
i = 1;
(i < position)
&&
(cursor != NULL);
++i
)
cursor = cursor->link();
return cursor;
}
```

- 26. The definition makes bag::value_type the same as node::value_type, so that a programmer can use bag::value_type without having to know the details of the linked-list implementation.

- 27. The value_type in the node class would need to be changed to string (as in the answer to Self-Test Exercise 13).

- 28. Assuming that we have set the bag's value_type to a string, we would write this code:
```cpp
bag exercise;
exercise.insert("squash");
exercise.insert("handball");
cout << exercise.grab() << endl;
cout << exercise.size() << endl;
```

- 29. Generally we will choose the approach that makes the best use of the previously written functions. This saves us work and also reduces the chance of new errors from writing new code to do an old job. The preference would change if writing new functions offered better efficiency.

- 30. The two lines of code that we have in mind are:
```cpp
p = p->link();
p = list_search(p, d);
```
These two lines are the same as the single line: p = list_search(p->link(), d);

- 31. When the target is not in the bag, the first assignment statement to cursor will set it to the null pointer. This means that body of the loop will not execute at all, and the function returns the answer zero.

- 32. The problem occurs when the target is the first item on the linked list. In this case, the target pointer is at the head of the list, so it would be a mistake to remove the head node before moving the target pointer forward.

- 33. The rand function from cstdlib generates a non-negative pseudorandom integer. A pseudorandom generator is advantageous for debugging a program because if the program is run again with the same initial conditions, the generator will produce exactly the same sequence of numbers.

- 34. (rand() % 21) - 10;

- 35. All the functions are constant time except for remove, grab, and count (which are all linear); the copy constructor and operator = (which are O(n), where n is the size of the bag being copied); the operator += (which is O(n), where n is the size of the addend); and the operator + (which is O(m+n), where m and n are the sizes of the two bags).

- 36. A precursor node pointer is necessary in the sequence class because its insert function adds a new item immediately before the current node. Because the linked-list toolkit's insert function adds an item after a specified node, the precursor node is designated as that node.

- 37. many_nodes is 3, and these are the other member variables:

![](img/7bf56f684fab50d5ff9e94ae2818f3ac_312_0.png)

- 38. First check that the item occurs somewhere in the list. If it doesn't, then return with no work. If the item is in the list, then set the current item to be equal to this item, and call the ordinary erase_one function.

- 39. The insert and attach functions both allocate dynamic memory, as do the copy constructor and assignment operator.

- 40. The copy constructor and assignment operator might use list_piece.

- 41. Arrays are quickest for random access.

- 42. Linked lists are quickest for insertions/deletions at a cursor.

- 43. A doubly linked list is best.

- 44. O(n), where n is the size of the array prior to resizing

- 45. See Figure 5.18 on page 286.

46. Here is one solution:
```cpp
void dlist_head_insert(
    dnode*& head_ptr,
    const dnode::value_type& entry
)
{
    dnode *insert_ptr;
    insert_ptr =
        new dnode(entry, head_ptr);
    if (head_ptr != NULL)
        head_ptr->set_back(insert_ptr);
    head_ptr = insert_ptr;
}
```

47.
```cpp
void move_to_front(
    vector<string>& data,
    vector<string>::size_type index
)
{
    assert(index > 0);
    assert(index <= data.size());
    string item = data[index]; // Save a copy
    for (i = index; i > 0; --i)
        data[i] = data[i-1];
    // Put the copy at the front of the vector:
    data[0] = item;
}
```

## FIGURE 5.18 Class Definition for a Node of Doubly Linked List

### A Class Definition

```cpp
class dnode
{
public:
    // TYPEDEF
    typedef double value_type;
    // CONSTRUCTOR
    dnode(
        const value_type& init_data = value_type(),
        dnode* init_fore = NULL,
        dnode* init_back = NULL
    )
    { data_field = init_data; link_fore = init_fore; link_back = init_back; }
    // Member functions to set the data and link fields:
    void set_data(const value_type& new_data) { data_field = new_data; }
    void set_fore(dnode* new_fore) { link_fore = new_fore; }
    void set_back(dnode* new_back) { link_back = new_back; }
    // Const member function to retrieve the current data:
    value_type data() const { return data_field; }
    // Two slightly different member functions to retrieve each current link:
    const dnode* fore() const { return link_fore; }
    dnode* fore() { return link_fore; }
    const dnode* back() const { return link_back; }
    dnode* back() { return link_back; }
private:
    value_type data_field;
    dnode *link_fore;
    dnode *link_back;
};
```

- For this project, you will use the bag class with the value_type being a string from the <string> facility. The bag class should include the grab function from Figure 5.13 on page 270. Use this class in a program that does the following:
  1. Asks the user for a list of 10 nouns.
  2. Asks the user for a list of 10 verbs.
  3. Prints some random sentences using the provided nouns and verbs.
  For example, if two of the nouns were “monkey” and “piano,” and two of the verbs were “eats” and “plays,” then we can expect any of these sentences:
  The monkey eats the piano.
  The monkey plays the piano.
  The piano eats the monkey.
  The piano plays the monkey.
  Needless to say, the sentences are not entirely sensible. Your program will need to declare two bag variables: one to store the nouns and one to store the verbs. Use an appropriate top-down design.

- Write a function that takes a linked list of items and deletes all repetitions from the list. In your implementation, assume that items can be compared for equality using ==

- Write a function with three parameters. The first parameter is a head pointer for a linked list of items, and the next two parameters are items x and y. The function should write to the screen all items in the list that are between the first occurrence of x and the first occurrence of y. You may assume that items can be compared for equality using ==

- Write a function with one parameter that is a head pointer for a linked list of items. The function reverses the order of the nodes so that the last node is first, the first node is last, and so forth. The head pointer is a reference parameter, so that after the function completes, this same pointer variable is pointing to the head of the reversed list.

- Write a function that has two linked-list head pointers as parameters. Assume that the linked list’s items are ordered by the < operator. On each list, every item is less than the next item on the same list. The function should create a new linked list that contains all the items on both lists, and the new linked list should also be ordered (so that every new item is less than the next item on the list). The next list item should appear on only one item (i.e., if the same item appears on both input lists, only one copy is placed in the newly constructed linked list). To eliminate duplicate items, you may assume that two items can be compared for equality using ==. The function should return a head pointer for the newly constructed list.

- Write a function that starts with a single linked list of items and a special value called the splitting value. Two item values can be compared using the < operator—but the items of the original linked list are in no particular order. The procedure divides the nodes into two linked lists: one containing all the nodes that contain an item less than the splitting value, and one that contains all the other nodes. If the original linked list had any repeated integers (i.e., any two or more nodes with the same item in them) then the new linked list that has this item should have the same number of nodes that repeat this item. It does not matter whether you preserve the original linked list or destroy it in the process of building the two new lists, but your comments should document what happens to the original linked list.

- Write a function that takes a linked list of integers and rearranges the nodes so that the integers stored are sorted into the order
