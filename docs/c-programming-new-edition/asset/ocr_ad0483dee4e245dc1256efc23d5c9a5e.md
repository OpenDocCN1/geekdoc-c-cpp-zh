is incremented and it attains the value which is in the 1st position and this is added to ‘add’ which already has a computed number and this added value is affixed to add which loses the previous value.

The above process is repeated until the condition is dissatisfied. The total is then divided by the number of elements, which is represented in line 15. And displayed in the subsequent output statement in line 16.

# 4.8. ARRAY INSIDE THE MEMORY

You must be well versed with the details of declaring, initializing, and retrieving an array. But what happens in the memory? Are the elements stored in a serial order or are they stored randomly? To answer the above queries consider on example:

```
int sal[5];
```

What are the activities that take place inside the memory when such a declaration is made? By now you must be aware of what the above statement does. The statement indicates that an array variable is to be created which is of an integer data type and the array can hold 5 elements. In the memory 10 bytes will be reserved because each integer will be 2 bytes long. Until the array is initialized with some numbers, this array will host some unrelated numbers. Once the array is initialized the elements are stored in a continuous manner.

Take a look at the tabular representation below:

2012 2014 2016 2018 2020 10 20 30–40 50

In the above table you can see that the numbers entered by the user are registered in a successive pattern and each element takes 2 bytes. This is exactly how it is represented in the memory of a computer. The number below the element location is the address of the location and each element has its unique address in the memory by which it is identified (Figure 4.1).

![](bbox=[0.3, 0.7, 0.8, 0.92])

Figure 4.1. Array inside the memory.