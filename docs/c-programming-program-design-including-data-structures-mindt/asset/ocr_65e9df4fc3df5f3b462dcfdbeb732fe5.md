The first two statements declare `first` and `second` pointer variables of type `int`. The third statement creates an array of 10 components, and the base address of the array is stored into `first` (see Figure 12-8). (Note that `first` together with the arrow indicates that `first` points to the allocated memory.)

![](bbox=[0.183, 0.171, 0.909, 0.23])

**FIGURE 12-8**  Pointer `first` and the array to which it points

Suppose that some meaningful data is stored in the array pointed to by `first`. To be specific, suppose that this array is as shown in Figure 12-9.

![](bbox=[0.183, 0.334, 0.909, 0.394])

**FIGURE 12-9**  Pointer `first` and its array

Next, consider the following statement:

```
second = first;        //Line A
```

This statement copies the memory address held by `first` into `second`. After this statement executes, both `first` and `second` point to the same array, as shown in Figure 12-10.

![](bbox=[0.183, 0.555, 0.909, 0.665])

**FIGURE 12-10**  `first` and `second` after the statement `second = first;` executes

Let us next execute the following statement:

```
delete [] second;
```

After this statement executes, the array pointed to by `second` is deleted. This action results in Figure 12-11.

![](bbox=[0.183, 0.825, 0.909, 0.918])

**FIGURE 12-11**  `first` and `second` after the statement `delete [] second;` executes