An object you acquire which is not received by calling a method with one of the aforementioned words in it, you don’t own. These objects can be used as much as you want within the current execution stack, but after you leave your current stack you cannot expect that they will remain available for your use.

When you receive an object from some other method call, you’re going to get back an object that has been “autoreleased.” I discuss autoreleasing later in this chapter, but the important point is that an autoreleased object will be released the next time your application exits its run loop. This release will likely happen as soon as you leave your current method. Don’t expect that object to live beyond the current method, for example, if you’re assigning it to a member variable, then you need to retain it.

When you increment the retain count on an object, either by allocating it, copying it, or retaining it, you are taking ownership of that object, and staking a claim on it. You are stating that you require access to this object for some indefinite period of time, and when you are finished with it, you will give up ownership of that object, and allow it to be destroyed.

# CAUTION

Although you are becoming the owner of an object by retaining it, ownership does not imply exclusivity. Others may own the object, as well. You are not the only person who could be accessing the object and changing its values.

# Using autorelease

I’ve already mentioned autorelease. The autorelease concept is central to Objective-C memory management. It enables Objective-C to solve a critical problem that has faced other languages, such as C++ and C: defining a standard “handoff” mechanism for objects returned from other methods and how the memory associated with them is managed.

For example, if you think about a C++ method or function that returns an object, who is the owner of that object? Is it the method that was called? Or is it the calling method? How do you handle the transfer of that memory from one owner to another without somehow having it all spill out onto the floor somewhere in between? C++ and C have handled that through a variety of means. For the most part, it’s been up to the individual developer to create and document whatever standard they want to follow. The end result is that when learning a new library, you also need to learn whatever memory management system it’s using as well. Some libraries might prefer smart pointers, while others might prefer known contracts, for example.

When Objective-C was faced with this problem, the developers of Objective-C created the concept of "autorelease". Autorelease is a method that you call on an object just like release. However, instead of immediately decrementing the retain count on the object, you can think of autorelease as a promise from the runtime that it will decrement the retain count the next time the application’s run loop exits. Typically, this happens when your current method exits. When the retain count is decremented in this manner, the object will be released just like normal.