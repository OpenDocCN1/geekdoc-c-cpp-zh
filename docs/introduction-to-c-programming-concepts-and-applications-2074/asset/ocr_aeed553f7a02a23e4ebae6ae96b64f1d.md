# // DESTRUCTOR FUNCTIONS

Destructors are functions that are called when it is time for an object to be removed from memory. The destructor function is meant to "clean up" when it's time to get rid of an object. In code, a destructor is declared just like constructor functions, except that a

```
~node() {
    if (!is_answer) {
        delete false_answer;
        delete true_answer;
    }
}
```

destructor starts with a tilde (~), after which comes the class name and parentheses with no parameters.

In particular, the destructor is the place to delete previously allocated dynamic memory. For example, your 20 Questions program keeps all the memory you allocated until the end of the program.

It is always good practice to free up any allocated memory in the same object that created it. This means that when it's time to

delete a node, you also need to delete its children branches, so you should define a destructor in this case.

The destructor will only need to call delete on the children if it is a question node, because answer nodes don't have any children, so you first check to see if it's a question node. If so, you'll call delete on each of the children. The destructor will then be called on those nodes, which will call the destructors on their children, and so on, all the way through the tree.

# // VECTORS: AN ALTERNATIVE TO DYNAMIC MEMORY ALLOCATION

Vectors are a way of indirectly allocating data on the heap without having to use pointers or the allocating and destructor commands for new and delete. All that work is hidden inside the vector class.

When a vector is first created, there is enough space allocated on the heap to hold all the data in the initialization, plus a little more. As you keep adding elements onto a vector, eventually the memory that was allocated gets used up.

But when the vector is finally "full," where it's used all the memory that was already allocated, it then goes through a process to

get more. It allocates double the amount of memory, copies all the old data into this new memory, and then deletes the old memory. Now it has twice as much memory to work with, so it should take even longer before that memory fills up. This can keep going as long as more data keeps being added to a vector.

If you find yourself wondering whether you should use a vector or write your own dynamic memory allocation, then use the vector! With a vector, you're still using the heap, but it's a little easier to use, and you're much less likely to run into major errors or problems that people tend to encounter when using pointers. ◆

# READINGS

+   a Stroustrup, Programming Principles and Practice Using C++, sections 17.4, 17.5, and 17.9.

b Lippman, Lajoie, and Moo, C++ Primer, chap. 12.