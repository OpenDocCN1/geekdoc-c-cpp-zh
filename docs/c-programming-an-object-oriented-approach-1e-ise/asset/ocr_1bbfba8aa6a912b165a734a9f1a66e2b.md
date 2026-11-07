# Searching for a Value

In array processing, we often need to search for a value. Although there are advanced and efficient algorithms to search an array, they require that the array is sorted. We show an elementary search here that can be used even when the array is not sorted. It is sometimes called a *linear search*. The value we are testing for is known as the *search argument*.

# EXAMPLE 8.8

Assume we want to find if any value in an array of size 100 is equal to a value entered at run time. We can use a *for* loop with two terminating conditions. The first assures that we do not go beyond the size of the array; the second tests if we have found the element we are looking for. If the search is successful, we have found the index of the element, which is what we are looking for.

```
```cpp
bool found = false;
for (int i = 0; (i < size) && (!found); i++)
{
    if (numbers[i] == value)
    {
        index = i;
        found = true;
    }
}
if (found)
{
    cout >> "The value was found at index: " << index;
}
else
{
    cout >> "The value was not found";
}
```
```

# 8.2.2 Modifying Operations

There are operations that may change the value of elements, the order of elements, or both.

# Swapping

The first operation we discuss is the one that swaps (exchanges) the contents of two elements. This exchange is often used in other operations such as sorting. Figure 8.8 shows the wrong approach and the right approach in swapping elements 1 and 3.

![](bbox=[0.244, 0.763, 0.836, 0.904])

**Figure 8.8** Wrong way and right way to swap two elements in an array