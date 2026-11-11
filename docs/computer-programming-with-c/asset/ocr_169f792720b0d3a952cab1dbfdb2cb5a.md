![](bbox=[0.121, 0.109, 0.856, 0.41])

# 6.2.1  Initializing an array at the time of creation

In the program given in Section 6.2, we have individually initialized each element of array a as shown below:

```
a[0]=10;
a[1]=20;
a[2]=30;
```

Instead of initializing one element of an array at a time, you can also initialize all the array elements together by specifying the values in curly brackets. However, such an initialization can only be applied at the time of creating an array and no later than that. For example, you could initialize array a at the same time when you created it as shown below:

```
int a[3] = {10,20,30};
```

Such an initialization is called **direct initialization** of the array and the array elements will be initialized as shown in Figure 6.6.

When an array is initialized at the time of creation, C/C++ keeps it optional to specify the size of the array. For example, the following statement which does not specify the size of an array will also work well:

![](bbox=[0.704, 0.718, 0.856, 0.813])

```
int a[] = {10,20,30}; /*Specifying size is optional when array is initialized at the time of creation*/
```

The compiler itself computes the size of this array, considering at the number of values initialized to it.