inal shared_ptr as its argument. You can also use the assignment operator (=) to create a shared_ptr to the same resource. Lines 34–35 print the reference count of the original shared_ptr to show that the count increased by one when we created the second shared_ptr. As mentioned earlier, changes made to the resource of a shared_ptr are “seen” by all shared_ptrs to that resource. When we change the title of the Book using bookPtr2 (line 38), we can see the change when using bookPtr (lines 39–41).

# *Manipulating shared_ptrs in an STL Container*

Next we demonstrate using shared_ptrs in an STL container. We create a vector of Books (line 44) and add four elements (recall that BookPtr is a typedef for a shared_ptr<Book>, line 10). Lines 51–53 print the contents of the vector. Then we sort the Books in the vector by title (line 56). We use the function compareTitles (lines 20–23) in the sort algorithm to compare the title data members of each Book alphabetically.

# *shared_ptr Custom Deleter*

Line 63 creates a shared_ptr with a custom deleter. We define the custom deleter function deleteBook (lines 13–17) and pass it to the shared_ptr constructor along with a pointer to a new instance of class Book. When the shared_ptr destroys the instance of class Book, it calls deleteBook with the internal book * as the argument. Notice that deleteBook takes a Book *, not a shared_ptr. A custom deleter function must take one argument of the shared_ptr’s internal pointer type. deleteBook displays a message to show that the custom deleter was called, then deletes the pointer. A primary use for custom deleters is when using third-party C libraries. Rather than providing a class with a constructor and destructor as a C++ library would, C libraries frequently provide one function that returns a pointer to a struct representing a resource and another that does the necessary cleanup when the resource is no longer needed. Using a custom deleter allows you to use a shared_ptr to keep track of the resource and still ensure it is freed correctly.

# *Resetting a shared_ptr*

We call the shared_ptr member function reset (line 64) to show the custom deleter at work. The reset function releases the current resource and sets the shared_ptr to NULL. If there are no other shared_ptrs to the resource, it’s destroyed. You can also pass a pointer or shared_ptr representing a new resource to the reset function, in which case the shared_ptr will manage the new resource. But, as with the constructor, you should only use a regular pointer returned by the new operator.

# *shared_ptrs Are Destroyed When They Go Out of Scope*

All the shared_ptrs and the vector go out of scope at the end of the main function and are destroyed. When the vector is destroyed, so are the shared_ptrs in it. The program output shows that each instance of class Book is destroyed automatically by the shared_ptrs. There is no need to delete each pointer placed in the vector.

# 23.6.2 weak_ptr: shared_ptr Observer

A weak_ptr points to the resource managed by a shared_ptr without assuming any responsibility for it. The reference count for a shared_ptr doesn’t increase when a weak_ptr references it. That means that the resource of a shared_ptr can be deleted while there are