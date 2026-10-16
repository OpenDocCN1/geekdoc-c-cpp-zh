longer exists, and will cause an error. We say, “aVariable2 goes out of scope at the end of the second stack frame which is at line 12.” Earlier in this chapter, I mention that variables store data in memory. The memory they use can be allocated on the stack, just as you see in this example. The memory associated with those variables is also freed when the variable goes out of scope. That is, when the variable no longer exists. However, memory for variables can also be allocated on what’s called “the heap,” which is a pool of memory that your application can allocate data from by itself and which your application has much greater power over. However, as they said in Spiderman, “With great power comes great responsibility.” You have to also be sure to free any memory you allocate on the heap. Listing 2.5 shows an example of allocating an object on the heap and then freeing it.

# Listing 2.5

# Allocating memory on the heap.

```
// this allocates the memory
SomeClass *aVariable = [[SomeClass alloc] init];

// do something with aVariable

[aVariable release]; // this frees the memory.
```

The code in this listing is demonstrating a concept that I spend a great deal of time on later, when I look at objects. For now, simply understand that the variable aVariable is having its memory allocated on the heap. This means that if we didn’t release that memory at the bottom of this listing, that memory would stick around and it would be what is commonly referred to as a memory leak. One of the key ways to tell if a variable has its memory allocated on the heap versus the stack is by looking to see if it is a pointer. The * operator in the declaration of the aVariable variable in the prior example indicates that this is a pointer. A pointer is a variable that points to another memory location.

Note that previously, all the variables we have worked with so far have not had the * operator before their names. This has meant that their memory was allocated on the stack. Although you can use the pointers that are strictly allocated on the stack, most often when you see pointers in Objective-C, it will be for variables that are allocated on the heap. The key is to look for some kind of allocation function like that shown here.

Pointers are a tough subject to get your head around, but I have a section coming up that delves into them in detail.

Earlier in this chapter, I describe global variables. Similarly, another word for a variable that is allocated on the stack is local variable. Local variables are ones that exist only within the local scope. The local scope is another phrase that means “the current stack frame.” Some other types