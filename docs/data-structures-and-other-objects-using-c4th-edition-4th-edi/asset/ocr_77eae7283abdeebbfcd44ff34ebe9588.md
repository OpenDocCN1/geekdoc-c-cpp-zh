There are two common ways to build an initial heap from the array. One method is relatively easy to program, and we will show that method here. A second, more efficient method requires more difficult programming, which we will outline in Programming Project 5 on page 680.

The simple approach to make_heap builds the heap one element at a time, starting at the front of the array. Initially we start with just one element, and this one element forms a small heap of one node. For example, we might start with the array shown here:

![](bbox=[0.35, 0.29, 0.65, 0.33])

the first array element forms a heap with one node

In this array, the area to the left of the vertical bar can be viewed as a heap with just one node, and the area to the right is still a jumble of random values.

The make_heap algorithm adds the array nodes to the heap one at a time. In our example, we will next add the 35 to the heap, resulting in the following

# FIGURE 13.6 Heapsort

# A Function Implementation

```
void heapsort(int data[], size_t n)
// Precondition: data is an array with at least n components.
// Postcondition: The elements of data have been rearranged so
// that data[0] <= data[1] <= ... <= data[n-1].
// Library facilities used: algorithm, cstdlib (using the namespace std)
// NOTE: The implementation also uses the two functions, make_heap and reheapify_down,
// which are discussed in the text.
{
    size_t unsorted;
    make_heap(data, n);
    unsorted = n;
    while (unsorted > 1)
    {
        --unsorted;
        swap(data[0], data[unsorted]);
        reheapify_down(data, unsorted);
    }
}
```