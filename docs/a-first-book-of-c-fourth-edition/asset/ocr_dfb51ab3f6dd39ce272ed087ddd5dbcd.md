```
{
    temp = num[j];
    num[j] = num[j-1];
    num[j-1] = temp;
    moves++;
}
}

return moves;
}
```

Here's the output produced by Program 7.12:

The sorted list, in ascending order, is:
5 10 22 32 45 67 73 98 99 101
18 moves were made to sort this list

As with the selection sort, the number of comparisons in a bubble sort is O(n²), and the number of required moves depends on the initial order of values in the list. In the worst case, when the data is in reverse sorted order, the selection sort performs better than the bubble sort. Both sorts require n(n - 1)/2 comparisons, but the selection sort needs only n - 1 moves, and the bubble sort needs n(n - 1)/2 moves. The additional moves the bubble sort requires result from the intermediate exchanges between adjacent elements to "settle" each element into its final position. In this regard, the selection sort is superior because no intermediate moves are necessary. For random data, such as that used in Programs 7.11 and 7.12, the selection sort generally performs equal to or better than the bubble sort.