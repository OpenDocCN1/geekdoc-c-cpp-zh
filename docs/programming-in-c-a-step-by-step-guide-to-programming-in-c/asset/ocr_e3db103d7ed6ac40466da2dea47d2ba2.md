When thinking about malloc, free, and dynamically-allocated memory in general, remember again the distinction between a pointer and what it points to. If you call malloc to allocate some memory, and store the pointer which malloc gives you in a local pointer variable, what happens when the function containing the local pointer variable returns? If the local pointer variable has automatic duration (which is the default, unless the variable is declared static), it will disappear when the function returns. But for the pointer variable to disappear says nothing about the memory pointed to! That memory still exists and, as far as malloc and free are concerned, is still allocated. The only thing that has disappeared is the pointer variable you had which pointed at the allocated memory. (Furthermore, if it contained the only copy of the pointer you had, once it disappears, you'll have no way of freeing the memory, and no way of using it, either. Using memory and freeing memory both require that you have at least one pointer to the memory!)

# 12.2.4 Reallocating Memory Blocks

Sometimes you're not sure at first how much memory you'll need. For example, if you need to store a series of items you read from the user, and if the only way to know how many there are is to read them until the user types some “end” signal, you'll have no way of knowing, as you begin reading and storing the first few, how many you'll have seen by the time you do see that “end" marker. You might want to allocate room for, say, 100 items, and if the user enters a 101st item before entering the “end" marker, you might wish for a way to say "uh, malloc, remember those 100 items I asked for? Could I change my mind and have 200 instead?"

In fact, you can do exactly this, with the realloc function. You hand realloc an old pointer (such as you received from an initial call to malloc) and a new size, and realloc does what it can to give you a chunk of memory big enough to hold the new size. For example, if we wanted the ip variable from an earlier example to point at 200 ints instead of 100, we could try calling

```
ip = realloc(ip, 200 * sizeof(int));
```

Since you always want each block of dynamically-allocated memory to be contiguous (so that you can treat it as if it were an array), you and realloc have to worry about the case where realloc can't make the old block of memory bigger