operator followed by the pointer that points to the dynamically created memory. Additionally, if the dynamically created memory is an array as opposed to a single variable, then empty subscripts [] are placed between the delete operator and the pointer, as in the following statement from the program:

```
```delete [] iPtr;```
```

While the delete operator operates on a pointer, the delete operator does not delete the pointer. Instead, the delete operator deletes the memory at the address pointed to by the pointer.

Note You should only use the delete operator with a pointer that points to dynamically created memory. Using the delete operator with a pointer that points to memory created on the stack rather than from the heap can lead to unpredictable results.

Finally, since the pointer is the only way to which you can refer to the dynamically allocated variable, you should not change the value of the pointer to point to a different address unless you first assign a different pointer to the dynamically allocated memory. Otherwise, you no longer have a way of accessing the dynamically created memory. The result would be a memory leak.

![](bbox=[0.139, 0.393, 0.874, 0.412])