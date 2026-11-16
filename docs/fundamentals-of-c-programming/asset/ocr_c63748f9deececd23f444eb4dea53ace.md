assignment operator.

+   • If the caller passes an rvalue, the compiler generates code that invokes the move constructor or move assignment operator.

The purpose of move construction is to efficiently move the resources held by the temporary object into the new object being created. We want to avoid making a copy of the temporary. Similarly, the purpose of move assignment is to efficiently move the resources held by the temporary object into an existing object without creating a new object. The copy constructor and copy assignment operator are designed to make copies.

It is safe to "steal" the resources of the temporary object because a temporary object is transient and cannot be used later within the program. Even though temporary objects are transient, they nonetheless are real, nameless objects. If the class of the temporary has a destructor, the object's destructor will execute when the temporary object's ephemeral life is over. This means that even though the move constructor and move assignment operator may move a temporary's resources into another object, they must leave the temporary in a well-defined state so that the temporary's destructor can do its job.

The following implements the move constructor for the IntList5 class:

```
// Move constructor takes possession of the temporary's list
IntList5::IntList5(IntList5&& temp): IntList5() {
  // Swap contents with the temporary
  std::swap(head, temp.head);
  std::swap(tail, temp.tail);
  std::swap(len, temp.len);
}
```

This move constructor delegates to the constructor that accepts no arguments. This initializes the head and tail pointers of this new object to nullptr and the len field to zero. Note that this represents an empty, but valid linked list object. The move constructor then exchanges the head and tail pointers and len variable of the object it is creating with those of the temporary. This effectively moves the temporary's list of nodes to this object and moves this object's empty, but valid, list of nodes to the temporary. When this copy constructor finishes, the temporary's life is over. Since its temporary still contains valid head and tail pointers (both now null) and len data (now zero), its destructor can execute successfully. Observe that nowhere in this copy constructor did we traverse a list of nodes copying each element individually. This means move construction of a list of 1,000,000 nodes requires no more time than move constructing an empty list.

Note that the parameter to the move constructor is not declared const. If it were declared const, it would not be possible to swap its contents with new object being created. Also, it is important that the code within the move constructor leaves the temporary object in a well-defined state because the temporary soon will be cleaned up by its destructor. Since the temporary's destructor will attempt to follow pointers to free any nodes remaining in its list, the copy constructor should not, for example, set the temporary's head pointer to some random address or set its len field to -1. That is exactly why we perform the swap operations; we replace the original contents of the temporary with those of a newly minted, empty list.

The move assignment operator is similar to the move constructor, except assignment, of course, does not begin with an initially empty object. We must ensure our move assignment operator does not leak memory from any preexisting list of nodes the object may contain.

The implementation of the move assignment operator for the IntList5 class looks very similar to the move constructor:

```
// Move assignment operator
```