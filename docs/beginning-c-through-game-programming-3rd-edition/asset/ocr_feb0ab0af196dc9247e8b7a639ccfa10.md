The statement calls the function intOnHeap(), which allocates a chunk of memory on the heap for an int and assigns 20 to it.

```
int* intOnHeap()
{
    int* pTemp = new int(20);
    return pTemp;
}
```

Then, the function returns a pointer to this chunk of memory. Back in main(), the assignment statement assigns the address of the chunk of memory on the heap to pHeap2. Next, I use the returned pointer to display the value.

```
cout << "*pHeap2: " << *pHeap2 << "\n\n";
```

# Hint

Up until now, if you wanted to return a value created in a function, you had to return a copy of the value. But by using dynamic memory, you can create an object on the heap in a function and return a pointer to the new object.

# Using the delete Operator

Unlike storage for local variables on the stack, memory that you’ve allocated on the heap must be explicitly freed. When you’re finished with memory that you’ve allocated with new, you should free it with delete. That’s what I do with the following line, which frees the memory on the heap that stored 10.

```
delete pHeap;
```

That memory is returned to the heap for future use. The data that was stored in it is no longer available. Next, I free some more memory, which frees the memory on the heap that stored 20.

```
delete pHeap2;
```

That memory is returned to the heap for future use, and the data that was stored in it is no longer available. Notice that there’s no difference, as far as delete is concerned, regarding where in the program I allocated the memory on the heap that I’m deleting.

# Trick

Because you need to free memory that you’ve allocated once you’re finished with it, a good rule of thumb is that every new should have a corresponding delete. In fact, some programmers write the delete statement just after writing the new statement whenever possible, so they don’t forget it.