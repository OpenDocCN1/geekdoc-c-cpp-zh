less than or equal to the pivot, and the other will contain only values greater than or equal to the pivot. So, if 8 is picked as the pivot, Fig. 12.6(b) shows the result at the end of the process.

The same process can then be reapplied exactly to the left-hand and right-hand parts separately. This reapplication of the same procedure leads to a recursive definition. The detail of the rearranging procedure is as follows. The index of the pivot value is chosen simply by evaluating

`(first + last) / 2`

where `first` and `last` are the indices of the initial and final elements in the array representing the list. A `left_arrow` and a `right_arrow` are then identified on the far left and the far right respectively. This can be seen in Fig. 12.6(c), where `left_arrow` and `right_arrow` initially represent the lowest and highest indices of the array components. Starting from the right, the `right_arrow` is moved left until a value less than or equal to the pivot is encountered. See Fig. 12.6(d).

Similarly, the `left_arrow` is moved right until a value greater than or equal to the pivot is encountered. Now, the contents of the two array components are swapped as can be seen in Fig. 12.6(e).

Now, continuing the movement of the `right_arrow` left till `a[right_arrow] <= pivot`, the position of the `right_arrow` is as shown in Fig. 12.6(f).

Having reached the status shown in Fig. 12.6(g), the contents of the `a[left_arrow]` and `a[right_arrow]` are interchanged. After this interchange, the contents of the elements are shown in Fig. 12.6(h).

The process of movement of the `left_arrow` and `right_arrow` stops only when the condition `left_arrow > right_arrow` becomes true. Since in Fig. 12.6(h), this condition is still False, we move `right_arrow` left again as shown in Fig. 12.6(i).

Having reached the status shown in Fig. 12.6(k), the contents of the `a[left_arrow]` and `a[right_arrow]` are interchanged. It is acceptable to exchange the pivot because pivot is the value itself, not the index. As before, the `right_arrow` is moved left and the `left_arrow` is moved right as shown in Fig. 12.6(l).

The procedure’s terminating condition `left_arrow > right_arrow` is now true, and the first subdivision of the list (i.e., array) is now complete.

Here, the quick sort procedure is coded as a recursive C function. This can be shown as follows.

```
void quick_sort(int list[], int left, int right)
{
    int pivot, left_arrow, right_arrow;
    left_arrow = left;
    right_arrow = right;
```

```
pivot = list[(left + right)/2];
do
{
    while(list[right_arrow] > pivot)
        right_arrow--;
    while(list[left_arrow] < pivot)
        left_arrow++;
    if(left_arrow <= right_arrow)
    {
        swap(list[left_arrow], list[right_arrow]);
        left_arrow++;
        right_arrow--;
    }
}while(right_arrow >= left_arrow);
if(left < right_arrow)
    quick_sort(list, left, right_arrow);
if(left_arrow < right)
    quick_sort(list, left_arrow, right);
}
```

# 12.12 ANALYSIS OF ALGORITHMS

One significant factor considered while designing algorithms is the algorithm’s efficiency. The efficiency of an algorithm is determined by the amount of time it takes to run the program and the memory space the program requires. In analyzing an algorithm, rather than a piece of code, the number of times ‘the principle activity’ of that algorithm is performed, should be predicted. For example, if one is analyzing a sorting algorithm, one might count the number of comparisons performed, and if it is an algorithm to find an optimal solution, one might count the number of times it evaluates a solution.

Complexity of an algorithm is a measure of the amount of time and/or memory space required by an algorithm for a given input. It is a function describing the efficiency of the algorithm in terms of the amount of data the algorithm must process. Usually, there are natural units for the domain and range of this function. The factor or parameters or fields whose values affect the number of operations performed is called the problem size or the input size. The following are the two main complexity measures of the efficiency of an algorithm:

**Time complexity**  It is a function that describes the amount of time an algorithm takes with respect to the amount of input provided to the algorithm. ‘Time’ can mean the number of memory accesses performed, the number of comparisons between integers, the number of times some inner loop is executed, or some other natural unit related to the amount of real time the algorithm will take. It is denoted as T(n) where n is the size of the input.

**Space complexity**  It is a function that describes the amount of memory (space) an algorithm takes with respect to the amount of input provided to the algorithm. Space complexity is sometimes ignored because the space used is minimal and