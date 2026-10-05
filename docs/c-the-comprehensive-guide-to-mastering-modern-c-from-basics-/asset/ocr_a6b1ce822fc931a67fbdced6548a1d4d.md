in this way and inject malicious code into the computer. Therefore, it is important to always protect the stack particularly carefully from itself and others.

# 20.4.2 The Heap

There are cases where an object needs to live longer than the scope in which it was defined. This is also possible: you then create the object *dynamically*. This is done with the new keyword.

new itself returns a *raw pointer*, but you have already been warned about this type of pointer several times in this book. Therefore, the first thing you should do with the result of *new* is to wrap it in a *smart pointer* like `unique_ptr` or `shared_ptr`. I will cover these smart pointers later in the chapter; in this section, we will discuss what dynamic memory is.

The object created with *new* does not end up on the stack, but on the *heap*. It stays there until you explicitly remove it with `delete` (which smart pointers do automatically). For this, you need its address, which you have stored in a pointer.

However, you must not clean up a heap object twice. If you copy the pointer to the object and store it in multiple places, it is very important that you designate exactly one of the pointers as the *owner* of the object and consider all others as *users*. The owner is responsible for removing it with `delete` at the appropriate time. With raw pointers, this owner is unfortunately only in the programmers' minds and hopefully in the documentation. There are several variants of smart