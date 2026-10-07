![](bbox=[0.165, 0.142, 0.735, 0.635])

Figure 17.6: Free Space With Two Chunks Allocated

bytes in after the three splits. But what happens when the calling program returns some memory via free()?

In this example, the application returns the middle chunk of allocated memory, by calling free(16500) (the value 16500 is arrived upon by adding the start of the memory region, 16384, to the 108 of the previous chunk and the 8 bytes of this chunk). This value is shown in the previous diagram by the pointer ptr.

The library immediately figures out the size of the free region, and then adds the free chunk back onto the free list. Assuming we insert at the head of the free list, the space now looks like this (Figure 17.6).