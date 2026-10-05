# 19 • More about Classes 615

```
MyArray f() {};
arr4 = f(); /* Because f() returns an rvalue move function is called. */
MyArray arr5 = f(); /* Because f() returns an rvalue move constructor is
called. */
```

If the move constructor and the move function are not declared in the class, the copy constructor and the copy function will be called instead. For example, in the arr4 = f() statement, the move function is not defined, the copy function will be called. If we use move() and no move assignment operator is defined, nothing happens; the copy assignment operator will be called instead. The same applies with the move constructor. If you use move() to construct an object (e.g., arr2 in the program) and the move constructor does not exist, the copy constructor will be called.

Let's see how the program works. In the case of arr2, since move() returns an rvalue, the move constructor is called, and a is bound to arr1. The type of a is an value reference; this makes sense in order to be bound the value argument. It also makes sense for the compiler to make the move constructor rather than the copy constructor, in order to bind the value argument to the value reference. The move constructor makes the pointer of the rvalue object arr2 to the memory that arr1.p points to. the memory ownership is transferred. As we discussed in Chapter 16, if we use assign arr1(e.g., cout << arr[0]) unpredictable problems may arise.

Notice that the original pointer must be set to null, otherwise we would have two pointers, the pointer of the object (i.e. a.p), point to the same dynamically allocated memory. Do we want that? Certainly not, we are aware of the dangerous consequences. For example, that memory will be released twice when the objects are destroyed. When we don't want this to happen, make the original nullptr null. As we know, when it is destroyed delete[] applied to a null pointer has no effect.

Just like a user copy constructor typically comes together with a copy assignment operator, a user move assignment operator is typically accompanied by a move constructor. When the right operand of the assignment operator is an rvalue, the compiler uses the move function rather than the copy function and the value argument is bound to the value reference. Therefore, to continue in our example, arr2 will be passed as an argument to the operators() move function. As the comments in the code explain, this function moves its data to the calling object, that is, to arr3.

As you see, in both functions we only copied the pointers, which is nothing compared to the cost of copying entire arrays. While the move constructor moves data from the right operand to the left, the move assignment moves data from argument (e.g., a) to the newly constructed object.

So, if you want your types (e.g., MyArray) to support operations for better performance, you need to write your move functions using value references. As we said, you need pay attention to the code you'll write, so that after moving, the source object goes into a state that its destructor can handle. For example, if the object contains a pointer to allocated memory (e.g., p), you should explicitly assign it nullptr moving the data, rather than assuming that it is assigned automatically. You must keep in mind that the responsibility for managing the memory now lies with the destination object. When this is destroyed it will release the memory. In general, a move operation source must remain in a valid state where it can be destroyed without any problem.

Before continue, did you notice the existence of the noexcept? Well, we'll discuss the noexcept keyword in Chapter 22. In brief, it mentions that a function does not throw exceptions. It recommends that the move constructor and the move assignment operator should be declared as noexcept, ensuring that they do not throw exceptions, which is truly true. It is typically true, because the main purpose of move operations is to save resources, not to allocate any new memory or perform other operations that might fail. Because a copy function may be called instead of the desired move function if the move function is not declared as noexcept, it is very important to consider them as.

![](bbox=[0.079, 0.981, 0.155, 0.996])