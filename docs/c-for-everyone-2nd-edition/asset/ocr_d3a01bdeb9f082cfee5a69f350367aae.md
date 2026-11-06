```
for (int i = pos; i < size of values - 1; i++)
{
    values[i + 1] = values[i];
}
```

**Practice It** Now you can try these exercises at the end of the chapter: R6.10, R6.13, P6.6, P6.16.

# Special Topic 6.1 — Sorting with the C++ Library

![](bbox=[0.136, 0.254, 0.243, 0.326])

You often want to sort the elements of an array or vector. Special Topic 6.2 shows you a sorting algorithm that is relatively simple but not very efficient. Efficient sorting algorithms are significantly more complex. Fortunately, the C++ library provides an efficient sort function. To sort an array with size elements, call

```cpp
sort(a, a + size);
```

To sort a vector values, make this call:

```cpp
sort(values.begin(), values.end());
```

To fully understand the curious syntax of these calls, you will need to know advanced C++ that is beyond the scope of this book. But don’t hesitate to call the sort function whenever you need to sort an array or vector.

To use the sort function, include the `<algorithm>` header in your program.

# Special Topic 6.2 — A Sorting Algorithm

![](bbox=[0.136, 0.51, 0.243, 0.583])

A *sorting algorithm* rearranges the elements of a sequence so that they are stored in sorted order. Here is a simple sorting algorithm, called **selection sort**. Consider sorting the following array values:

![](bbox=[0.549, 0.547, 0.661, 0.578])

An obvious first step is to find the smallest element. In this case the smallest element is 5, stored in values[3]. You should move the 5 to the beginning of the array. Of course, there is already an element stored in values[0], namely 11. Therefore you cannot simply move values[3] into values[0] without moving the 11 somewhere else. You don’t know where the 11 should end up, but you know for certain that it should not be in values[0]. Simply get it out of the way by swapping it with values[3]:

![](bbox=[0.549, 0.677, 0.661, 0.719])

Now the first element is in the correct place. In the foregoing figure, the darker color indicates the portion of the array that is already sorted.

Next take the minimum of the remaining entries values[1] . . . values[4]. That minimum value, 9, is already in the correct place. You don’t need to do anything in this case, simply extend the sorted area by one to the right:

![](bbox=[0.549, 0.804, 0.661, 0.823])

Repeat the process. The minimum value of the unsorted region is 11, which needs to be swapped with the first value of the unsorted region:

![](bbox=[0.549, 0.865, 0.661, 0.905])