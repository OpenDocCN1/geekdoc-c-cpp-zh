
```cpp
Node* n1 = new Node(arg1, arg2);
// ... 
delete p;
Node* n2 = new Node(arg3, arg4);
// ... 
}
```

Each time around the loop we create two Nodes, and in the process of doing so we create a Message and delete it again. Such code would be unusual as part of building a data structure based on input from some “device.” Looking at this code, we might expect to “consume” 2\*sizeof(Node) bytes of memory (plus free-store overhead) each time around the loop. Unfortunately, it is not guaranteed that the “consumption” of memory is restricted to the expected and desired 2\*sizeof(Node) bytes. In fact, it is unlikely to be the case.

Assume a simple (though not unrealistic) memory manager. Assume also that a Message is a bit larger than a Node. We can visualize the use of free space like this, using orange for the Message, green for the Nodes, and plain white for “a hole” (that is, “unused space”):

![](img/e0ceba017429f80f5cf63e81a1e7ef4f_969_0.png)
![](img/e0ceba017429f80f5cf63e81a1e7ef4f_969_1.png)
![](img/e0ceba017429f80f5cf63e81a1e7ef4f_969_2.png)
![](img/e0ceba017429f80f5cf63e81a1e7ef4f_969_3.png)
![](img/e0ceba017429f80f5cf63e81a1e7ef4f_969_4.png)
![](img/e0ceba017429f80f5cf63e81a1e7ef4f_969_5.png)

So, we are leaving behind some unused space (“a hole”) on the free store each time we execute the loop. That may be just a few bytes, but if we can’t use those holes it will be as bad as a memory leak – and even a small leak will eventually kill a long-running program. Having the free space in our memory scattered in many “holes” too small for allocating new objects is called memory fragmentation. Basically, the free-store manager will eventually use up all “holes” that are big enough to hold the kind of objects that the program uses, leaving only holes that are too small to be useful. This is a serious problem for essentially all long-running programs that use **new** and **delete** extensively; it is not uncommon to find unusable fragments taking up most of the memory. That usually dramatically increases the time needed to execute **new** as it has to search through lots of objects and fragments for a suitably sized chunk of memory. Clearly this is not the kind of behavior we can accept for an embedded system. This can also be a serious problem in naively designed non-embedded systems.

Why can't “the language” or “the system” deal with this? Alternatively, can’t we just write our program to not create such “holes”? Let’s first examine the most obvious solution to having all those little useless “holes” in our memory: let’s move the **Nodes** so that all the free space gets compacted into one contiguous area that we can use to allocate more objects.

Unfortunately, “the system” can’t do that. The reason is that C++ code refers directly to objects in memory. For example, the pointers **n1** and **n2** contain real memory addresses. If we moved the objects pointed to, those addresses would no longer point to the right objects. Assume that we (somewhere) keep pointers to the nodes we created. We could represent the relevant part of our data structure like this:

![](img/e0ceba017429f80f5cf63e81a1e7ef4f_970_0.png)

Now we compact memory by moving an object so that all the unused memory is in one place:

![](img/e0ceba017429f80f5cf63e81a1e7ef4f_970_1.png)

Unfortunately, we now have made a mess of those pointers by moving the objects they pointed to without updating the pointers. Why don’t we just update the pointers when we move the objects? We could write a program to do that, but only if we knew the details of the data structure. In general, “the system” (the C++ run-time support system) has no idea where the pointers are; that is, given an object, the question “Which pointers in the program point to this object right now?” has no good answer. Even if that problem could be easily solved, this approach (known as *compacting garbage collection*) is not always the right one. For example, to work well, it typically requires more than twice the memory that the program ever needs to be able to keep track of pointers and to move objects around in. That extra memory may not be available on an embedded system. In addition, an efficient compacting garbage collector is hard to make predictable.

We could of course answer that “Where are the pointers?” question for our own data structures and compact those. That would work, but a simpler approach is to avoid fragmentation in the first place. In the example here, we could simply have allocated both **Nodes** before allocating the message:

```cpp
while(...){
    Node* n1 = new Node;
    Node* n2 = new Node;
    Message* p = get_input(dev);
    //... store information in nodes ...
    delete p;
    // ...
}
```

However, rearranging code to avoid fragmentation isn’t easy in general. Doing so reliably is at best very difficult and often incompatible with other rules for good code. Consequently, we prefer to restrict the use of the free store to ways that don’t cause fragmentation in the first place. Often, preventing a problem is better than solving it.

## TRY THIS

Complete the program above and print out the addresses and sizes of the objects created to see if and how “holes” appear on your machine. If you have time, you might draw memory layouts like the ones above to better visualize what’s going on.

### 25.3.2 Alternatives to the general free store

So, we mustn’t cause fragmentation. What do we do then? The first simple observation is that **new** cannot by itself cause fragmentation; it needs **delete** to create the holes. So we start by banning **delete**. That implies that once an object is allocated, it will stay part of the program forever.

In the absence of **delete**, is **new** predictable; that is, do all **new** operations take the same amount of time? Yes, in all common implementations, but it is not actually guaranteed by the standard. Usually, an embedded system has a startup sequence of code that establishes the system as “ready to run” after initial power-up or restart. During that period, we can allocate memory any way we like up to an allowed maximum. We could decide to use new during startup. Alternatively (or additionally) we could set aside global (static) memory for future use. For reasons of program structure, global data is often best avoided, but it can be sensible to use that language mechanism to pre-allocate memory. The exact rules for this should be laid down in a coding standard for a system (see §25.6).

There are two data structures that are particularly useful for predictable memory allocation:

- *Stacks*: A stack is a data structure where you can allocate an arbitrary amount of memory (up to a given maximum size) and deallocate the last allocation (only); that is, a stack can grow and shrink only at the top. There can be no fragmentation, because there can be no “hole” between two allocations.
- *Pools*: A pool is a collection of objects of the same size. We can allocate and deallocate objects as long as we don’t allocate more objects than the pool can hold. There can be no fragmentation because all objects are of the same size.

For both stacks and pools, both allocation and deallocation are predictable and fast.

So, for a hard real-time or critical system we can define stacks and pools as needed. Better yet, we ought to be able to use stacks and pools as specified, implemented, and tested by someone else (as long as the specification meets our needs).

Note that the C++ standard containers (**vector**, **map**, etc.) and the standard string are not to be used because they indirectly use new. You can build (buy or borrow) “standard-like” containers to be predictable, but the default ones that come with your implementation are not constrained for embedded systems use.

Note that embedded systems typically have very stringent reliability requirements, so whatever solution we choose, we must make sure not to compromise our programming style by regressing into using lots of low-level facilities directly. Code that is full of pointers, explicit conversions, etc. is unreasonably hard to guarantee as correct.

### 25.3.3 Pool example

A *pool* is a data structure from which we can allocate objects of a given type and later deallocate (free) such objects. A pool contains a maximum number of objects; that number is specified when the pool is created. Using green for “allocated object” and blue for “space ready for allocation as an object,” we can visualize a pool like this:

![](img/e0ceba017429f80f5cf63e81a1e7ef4f_972_0.png)
