To solve this problem, there is another kind of lock called NSRecursiveLock. This lock keeps track of the thread which has locked it, and if that thread attempts to lock it again, it simply returns immediately. You do not need to be concerned about accessing the data which you are yourself locking from your existing thread. Therefore, attempting to lock a lock which you already have a lock on doesn’t make any sense. Using an NSRecursiveLock in these cases resolves this problem.

# Using the @synchronize keyword

Using locks is a simple and efficient way to ensure that your code is thread safe. However, you may find, after you’ve written a certain amount of NSLock based code, certain patterns begin to emerge.

The first pattern is that you often want to lock access to specific variables, or all member variables of a particular object, and so you have instances of locks that are associated with these specific variables. Often, you have a lock that uses a member of a given class as its lock object. You might lock this lock whenever you need to access any of the data in that class. Alternatively, you might have particular locks associated with particular variables, and you want to make sure that you lock those locks whenever those particular variables are accessed. In other words, you are trying to protect the coupling between the data. Ideally, you’d like to have some kind of language construct that enabled you to express this relationship in your code.

The second pattern that tends to emerge when working with thread locks is the fact that it is easy to forget to unlock your locks. When this occurs, you wind up with deadlock situations that can really ruin your day. This can be especially problematic when exceptions are introduced, causing situations where normal execution of the call stack might be interrupted. Because of these problems, Objective-C introduced a built-in language directive called @synchronized. This directive provides a built in low-level mutually exclusive lock mechanism which also includes specific scoping and variable parameters. What this means is that the @synchronized directive gives you the ability to specify a lock for a specific variable and to specify that lock exists for a particular scope of code. Listing 16.3 shows an example of the @synchronized directive in use.

# Listing 16.3

# Using @synchronized

```
- (void)setSomeVar: (id) inValue
{
    [inValue retain];
    @synchronized(someVar)
    {
```