![](bbox=[0.31, 0.13, 0.73, 0.6])

Fig. 6.21 Number 17 is inserted into the heap from Fig. 6.19. Since it is smaller than the value 21 stored at parent node, numbers 17 and 21 are exchanged. The 17 is exchanged with number 19. Since 17 is not smaller than the number 15 stored at the root, it comes to rest.

```
    11    while(pos > 0)&&
    12        (heap[parent].t > heap[pos].t))
    13    {
    14        elem = heap[parent];                 /* exchange parent/child */
    15        heap[parent] = heap[pos];
    16        heap[pos] = elem;
    17        pos = parent;                         /* move up */
    18        parent = (pos-1)/2;
    19    }
    20  }
```

In lines 6–9 the new element is inserted at the end and the number of elements is increased by one. In lines 10–19 the new element is moved (lines 14–16) towards the root until the current parent is smaller than the new element or until the root is reached (lines 11–12). Note that in case one wants to implement double bookkeeping (see page 194), one would have to update the pointers, which point to an element in the heap from outside, whenever an element is moved. Hence, in this case the data structure which holds the pointers would have to be passed to the function as well.