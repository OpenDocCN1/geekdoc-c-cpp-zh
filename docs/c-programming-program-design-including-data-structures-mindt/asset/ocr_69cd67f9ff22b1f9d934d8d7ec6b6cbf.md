This statement declares **myList** to be an array of five components of type **int**. The components are **myList[0]**, **myList[1]**, **myList[2]**, **myList[3]**, and **myList[4]**. The computer allocates five memory spaces, each large enough to store an int value, for these components. Moreover, the five memory spaces are contiguous.

The base address of the array **myList** is the address of the component **myList[0]**. Suppose that the base address of the array **myList** is 1000. Then, the address of the component **myList[0]** is 1000. Typically, the memory allocated for an int variable is four bytes. Recall from Chapter 1 that main memory is an ordered sequence of cells, and each cell has a unique address. Typically, each cell is one byte. Therefore, to store a value into **myList[0]**, starting at the address 1000, the next four bytes are allocated for **myList[0]**. It follows that the starting address of **myList[1]** is 1004, the starting address of **myList[2]** is 1008, and so on (see Figure 8-7).

![](bbox=[0.183, 0.349, 0.909, 0.756])

**FIGURE 8-7**  Array *myList* and the addresses of its components

Now **myList** is the name of an array. There is also a memory space associated with the identifier **myList**, and the base address of the array is stored in that memory space. Consider the following statement:

```
cout << myList << endl;        //Line 2
```

Earlier, we said that this statement will not give the desired result. That is, this statement will not output the values of the *components* of **myList**. In fact, the statement