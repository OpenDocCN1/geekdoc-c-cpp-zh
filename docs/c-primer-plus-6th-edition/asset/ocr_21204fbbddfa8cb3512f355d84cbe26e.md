# Generic Programming

So let's look at searching another kind of data structure, the linked list. (Chapter 12 uses a linked list to implement a Queue class.) The list consists of linked Node structures:

```
struct Node
{
  double item;
  Node *p_next;
}
```

Suppose you have a pointer that points to the next node, and the p_next pointer in each node points for the last node in the list is set to 0. You could write a find_ll() function like this:

```
Node* find_ll(Node * head, const double & val)
{
  Node * start;
  for (start = head; start != 0; start = start->p_next)
    if (start->item == val)
      return start;
  return 0;
}
```

Again, you could use a template to generalize this to lists of any data type supporting the == operator. Nonetheless, this algorithm is still tied to one particular data structure—the linked list.

If you consider details of implementation, the two functions use different algorithms: One uses array indexing to move through a list of items, and the other resets to start->p_next. But broadly, the two algorithms are the same: Compare the value with each value in the container in sequence until you find a match.

The goal of generic programming in this case would be to have a single function that would work with arrays or linked lists or any other container type. It is, not only the function be independent of the data type stored in the container, but provide a generic representation for the data type stored in a container. What's needed a generic representation of the process of moving through the values in a container. The iterator is that generalized representation.

What properties should an iterator have in order to implement a find function? Here's a short list:

+   * You should be able to dereference an iterator in order to access the value to which it refers. That is, if p is an iterator, *p should be defined.

+   * You should be able to assign one iterator to another. That is, if p and q are iterators, the expression p = q should be defined.

+   * You should be able to compare one iterator for another for equality. That is, if p and q are iterators, the expressions p == q should be defined.