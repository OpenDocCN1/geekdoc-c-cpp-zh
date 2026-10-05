# Operator Overloading, Type Conversion, New Style Casts, and RTTI

![](bbox=[0.305, 0.093, 0.765, 0.373])

**Figure 8.2** Wastage of memory due to the default action of the new operator

* A * APtr = new A;

we get Part A and not Part B of Figure 8.2 (suppose objects of class A occupy 10 bytes)
This means every time the new operator is called for the class A, a separate block to store the memory of allocated will be allocated. This consumption of memory can be a real bottleneck in applications where memory is critical.

Before we come to a solution to this problem, we should know that even if the ‘new’ operator allocates array of objects, only one memory will be prefixed to the allocated memory block in order to hold its size. Therefore, the amount of extra memory allocated remains the same whether one object is created in the heap or an array of objects is created in the heap. The class designer can take advantage of this fact.

The class designer can ensure that when the new operator is called for the first time, a memory to hold a large number of objects gets allocated and the address of the memory block pool. The address returned will obviously be the address of the first object in the pool. Thereafter, every call to the new operator will return the address of the next available block from the pool.

This solution is explained in Figures 8.3 and 8.4. Suppose A is a class objects occupy 10 bytes. The class designer reckons that the pool will hold five objects at a time. Therefore, the pool size will be equal to 50 bytes. Let us consider the piece of code given in Listing 8.47.

+   **Listing 8.47** Calling an overloaded new operator

```
...
A * APtr1 = new A; //line 1
A * APtr2 = new A; //line 2
A * APtr3 = new A; //line 3
A * APtr4 = new A; //line 4
A * APtr5 = new A; //line 5
A * APtr6 = new A; //line 6
```