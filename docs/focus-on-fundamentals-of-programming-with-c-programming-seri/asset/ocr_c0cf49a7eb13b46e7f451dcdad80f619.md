We copy the data item to be sorted into a temporary location, thereby opening a possible insertion point in the sorted array for the data item:

![](bbox=[0.06, 0.115, 0.68, 0.205])

3 < 5 so we must open a new insertion point. We shift 5 to the right one position opening a new insertion point:

![](bbox=[0.06, 0.3, 0.68, 0.39])

Reaching the start of the array tells us that the current insertion point is valid as the new data item is the smallest data item seen so far. So we insert the data item into the insertion point:

![](bbox=[0.06, 0.52, 0.68, 0.61])

At the end of the 1st pass, the first 2 data items are sorted.

We begin the 2nd pass. The next data item to sort is 8:

![](bbox=[0.06, 0.75, 0.68, 0.84])