Figure 8-10 shows the elements of `list` in the first iteration.

Initially, the entire list is unsorted. So, we find the smallest item in the list. The smallest item is at position 6, as shown in Figure 8-10(a). Since this is the smallest item, it must be moved to position 0. So, we swap 16 (that is, `list[0]`) with 5 (that is, `list[6]`), as shown in Figure 8-10(b). After swapping these elements, the resulting list is as shown in Figure 8-10(c).

![](bbox=[0.182, 0.22, 0.909, 0.472])

FIGURE 8-10  Elements of list during the first iteration

Figure 8-11 shows the elements of list during the second iteration.

Now the unsorted list is `list[1]...list[7]`. So, we find the smallest element in the unsorted list. The smallest element is at position 3, as shown in Figure 8-11(a). Because the smallest element in the unsorted list is at position 3, it must be moved to position 1. So, we swap 7 (that is, `list[3]`) with 30 (that is, `list[1]`), as shown in Figure 8-11(b). After swapping `list[1]` with `list[3]`, the resulting list is as shown in Figure 8-11(c).

![](bbox=[0.182, 0.672, 0.909, 0.915])

FIGURE 8-11  Elements of list during the second iteration