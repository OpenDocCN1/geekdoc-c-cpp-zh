# How Insertion Sort Works?

We take an unsorted array for our example.

![](bbox=[0.05, 0.12, 0.52, 0.15])

Insertion sort compares the first two elements.

![](bbox=[0.05, 0.18, 0.52, 0.21])

It finds that both 14 and 33 are already in ascending order. For now, 14 is in sorted sublist.

![](bbox=[0.05, 0.24, 0.52, 0.27])

Insertion sort moves ahead and compares 33 with 27.

![](bbox=[0.05, 0.3, 0.52, 0.33])

And finds that 33 is not in the correct position.

![](bbox=[0.05, 0.36, 0.52, 0.39])

It swaps 33 with 27. It also checks with all the elements of sorted sub-list. Here we see that the sorted sub-list has only one element 14, and 27 is greater than 14. Hence, the sorted sub-list remains sorted after swapping.

![](bbox=[0.05, 0.5, 0.52, 0.54])

By now we have 14 and 27 in the sorted sub-list. Next, it compares 33 with 10.

![](bbox=[0.05, 0.6, 0.52, 0.63])

These values are not in a sorted order.

![](bbox=[0.05, 0.66, 0.52, 0.69])

So we swap them.

![](bbox=[0.05, 0.72, 0.52, 0.75])

However, swapping makes 27 and 10 unsorted.

![](bbox=[0.05, 0.78, 0.52, 0.81])

Hence, we swap them too.

![](bbox=[0.05, 0.84, 0.52, 0.87])

Again we find 14 and 10 in an unsorted order.