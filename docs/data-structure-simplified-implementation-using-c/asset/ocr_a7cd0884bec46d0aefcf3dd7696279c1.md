![](bbox=[0.223, 0.107, 0.875, 0.244])

In the above statement, number is acting as an array identifier. Here an array of integer type is created, that is capable to store 10 integer type numbers. If we assume that the size of integer is 2; also assume that first address of an array is 3000 then we can compute the address of subsequent elements. Address computation of various elements of an array has been illustrated in the figure 2.1.

In an array, elements are placed one after another; however, storage at any index/subscript is possible. For instance, if the order of arrival of elements is 15, 10, and 7 then it is not mandatory that they have to be stored in the index 0, 1, 2 respectively. We can store them at any index of an array based on the availability. For instance, the first element can be stored in the array index 2, 10 at index 1 and the element 7 at the index number 0. Initialization of these elements is as follows:

```
array [2] =15;

array [0] =10;

array [1] =7.
```

However, as a good practice, it is suggested to use the contiguous address for storage. Correspondingly, to access an array element stored at 4ᵗʰ index, syntax array [4] need to be used. It is worth mentioning that the element that is stored at 5ᵗʰ location of an array will be accessed (Since index starts from 0). For instance, if the array is given as **int array1 = {4, 9, 12, 67, 90, 45}**, in this case, array1 [4] will be 90. Since, the index 4 which is 5ᵗʰ element of an array has value of 90.

![](bbox=[0.178, 0.7, 0.868, 0.826])

Array offers number of advantages such as it eliminates the need of creating many variables. Consequently, complexity of the program is reduced to a great extent. The other advantage is array is fast relative to the dynamically allocated variables. Following program demonstrates