pool will be deallocated when that autorelease pool is drained. Again, autorelease pools are a useful tool to aid in making manual memory management easier. They are not to be confused with automatic memory management.

In the next section, I explain how memory management looks from inside your objects and what you need to do to make sure that your object is managing its resources correctly.

# Understanding memory from inside the object

You may be wondering what happens to your objects when you are allocating and releasing them." When someone instantiates one of your objects, they call your init method. When they release one of your objects, your dealloc method is called automatically by the runtime. When allocating and initializing a new object, your initializer should allocate and initialize all of the member variables of that object. Similarly, when releasing an object, your dealloc method should release all of the allocated memory both from your objects initializer as well as any dynamic memory that may have been allocated during execution of any of the methods on that object. Essentially, when initializing a new object, you allocate whatever resources that object will require, and when releasing the object you should deallocate those resources.

CAUTION
You should never call dealloc yourself.

You’ve already seen that when you create a new object, and assign it to a variable, you call alloc on the class which in turn, returns an allocated object, with no data members. You then use that object to call init, or another initializer that is appropriate for your class. The initializer is where you allocate the memory for your member variables in your object.

The dealloc method is never called directly by you. It is called indirectly, when you call the release method on your object. The dealloc method is also called automatically when your object is released by an autorelease pool.

How you allocate and deallocate memory inside of these methods is important. I go into to detail in the next section.

# Writing initializers

When writing initializers, remember to call either the designated initializer for your class or call the superclass’ designated initializer.

To call the designated initializer for your current class, you call it by using the special variable, self, like so: [self init]. To call the superclass’s designated initializer, you use the special variable super, and call the superclass’s designated initializer by calling [super init]. Both