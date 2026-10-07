# Listing 13–3. Memory Allocation with ARC.

```
1 int main(void)
2 {
3 char *data2 = malloc(100);
4 NSString *myString = [[NSString alloc init];
5 // standard "doing-stuff" ellipse
7 free(data2); // Deallocate the 100 bytes
8 data2 = NULL;
9 myString = nil;
10 }
```

The major difference between Listing 13–2 and Listing 13–3 is the omission of [myString release]. Since ARC is being used, it handles the releasing of the memory.

# Using Special Pointers

As you've learned, a pointer is just a number that represents an address to memory. There are two special pointers that are worth mentioning. They aren't really pointers per, but they represent an empty pointer—a pointer that doesn't point to anything. These two pointers are NULL and nil. NULL is nothing more than zero, zinc, nada. Since pointers are just numbers that represent an address, an address of 0, represents a pointer that logically points to nothing.

Using an address of zero is a convention that modern computers use; computers do not allow any pointer to store something at the address 0, which makes NULL to represent an empty or unused piece of memory much more meaningful. This is important to know because if memory allocation fails, the resulting pointer returned is NULL. NULL is also useful to indicate that the pointer is no longer valid or simply empty. This is true for all of Standard C. Here's how NULL can be used to initialize a pointer:

```
char *data = NULL;
```

It should also be used in comparisons like the code fragment in Listing 13–4.

# Listing 13–4. NULL to malloc(100).

```
1 char *data = malloc(100);
2 if (data != NULL) {
3 // Do something with the memory. It's valid.
4 free(data); // Deallocate the memory, we're done with it.
5 data = NULL; // Set the pointer to NULL indicating that it's empty.
6 }
```

In Listing 13–4, line 2 checks to make sure that the malloc functioned by checking the pointer with NULL. If the pointer is not NULL, the allocation worked and the program can use the returned value. The memory is deallocated on line 4 and line 5 to indicate that the pointer is no longer pointing to anything.

When we are dealing with Objective-C objects, the equivalent of NULL in Objective-C is nil. Like NULL, nil is a special pointer to nothing. However, in the case of Objective-C, nil is actually an empty object. Objective-C is heavy on sending messages to an object, an empty pointer should respond to it, even if pointer is