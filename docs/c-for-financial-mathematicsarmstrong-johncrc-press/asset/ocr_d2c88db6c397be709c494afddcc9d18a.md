I ran the code above on a 32-bit computer and got the following output:

Memory location of myVariable 0013FE78
Value of myVariable 10

Notice that `pointerToMyVariable` is a pointer to an int, so it is of type `int*`. Since `myVariable` is an int, `&myVariable` is a pointer to an int.

Since `pointerToMyVariable` is a pointer to an int, `*pointerToMyVariable` is an int.

It is worth emphasising that we use `&` in two completely different ways. We've used this symbol previously for pass by reference. We're using it now to convert a variable into a pointer. These uses are completely unconnected. It just happens to be the same character. When used as part of a type definition, `&` means “reference”. When used as an operator, `&` means “memory location of”.

We also use `*` in three different ways. We use it in type definitions to mean “this is a pointer”. We use it to convert pointers back to references. And (in case you'd forgotten) we also use it for multiplication!

Another very useful operator for working with pointers is `->`. You can use `->` to access the fields of an object via a pointer.

```
```cpp
  Pair p;
  Pair* pointerToP = &p;

  // Use -> to access fields via a pointer
  pointerToP->x = 123.0;
  pointerToP->y = 456.0;

  // We check that c has changed
  ASSERT( p.x==123.0 );
  ASSERT( p.y==456.0 );

  // You could use * and .
  ASSERT( (*pointerToP).x==123.0 );
  ASSERT( (*pointerToP).y==456.0 );
```
```

Using `->` is equivalent to using `*` and `.` in combination but is easier to read.

You can also add and subtract integers to a pointer. For example, if `p` is a pointer to a memory location, then `p+1` is a pointer to the next memory location, and `p+3` is a pointer to three memory locations along. This is illustrated in Figure 11.2. To add one to a pointer, you can write `p++`. Working with pointers in this way is called *pointer arithmetic*.

# ### 11.2.3 Looping with pointers

We can pass a pointer to a function much as we pass an array to a function. Indeed, there isn't really any difference between a function that takes an array