The root is stored in heap[0] and the last node in heap[maxnodes], where maxnodes is the number of nodes in the heap. We may note that for any node heap[i], its two children reside in heap[i x 2 + 1] and heap[i x 2 + 2]. If we want to know the parent of any node[k], we can get it at the node[(k – 1)/2].

Now, let us write an algorithm as shown in Algorithm 12.1 to create a heap of size i by adding a key to a heap of size i – 1 where i ≥ 1.

# ALGORITHM 12.1

```
s = i;
/* find the parent node of i in the array * /
parent = (s – 1)/2;
key[s] = newkey;
while(s > 0 && key[parent] <= key[s])
{
/* interchange parent and child * /
temp = key[parent];
key[parent] = key[s];
key[s] = temp;
/* advance one level up in the tree * /
s = parent;
parent = (s – 1)/2;
}
```

This algorithm is called for each addition of a new key to the heap.

For example, consider the following unsorted list of keys.

+   8, 20, 9, 4, 15, 10, 7, 22, 3, 12

Figures 12.26(a)-(j) show the building of a heap using this list of keys.

![](bbox=[0.5, 0.6, 0.6, 0.65])

![](bbox=[0.35, 0.65, 0.6, 0.75])

![](bbox=[0.6, 0.65, 0.8, 0.75])

![](bbox=[0.25, 0.75, 0.45, 0.9])

![](bbox=[0.6, 0.75, 0.85, 0.9])