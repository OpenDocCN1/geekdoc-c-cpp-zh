```
Array a before make_heap:
3 100 52 77 22 31 1 98 13 40
Array a after make_heap:
100 98 52 77 40 31 1 3 13 22
Array a after sort_heap:
1 3 13 22 31 40 52 77 98 100

Array init contains: 3 100 52 77 22 31 1 98 13 40

v after push_heap(init[0]): 3
v after push_heap(init[1]): 100 3
v after push_heap(init[2]): 100 3 52
v after push_heap(init[3]): 100 77 52 3
v after push_heap(init[4]): 100 77 52 3 22
v after push_heap(init[5]): 100 77 52 3 22 31
v after push_heap(init[6]): 100 77 52 3 22 31 1
v after push_heap(init[7]): 100 98 52 77 22 31 1 3
v after push_heap(init[8]): 100 98 52 77 22 31 1 3 13
v after push_heap(init[9]): 100 98 52 77 40 31 1 3 13 22

v after 100 popped from heap
98 77 52 22 40 31 3 13 100
v after 98 popped from heap
77 40 52 22 13 31 1 3 98 100
v after 77 popped from heap
52 40 31 22 13 1 3 77 98 100
v after 52 popped from heap
40 22 31 1 3 52 77 98 100
v after 40 popped from heap
31 22 3 1 13 40 52 77 98 100
v after 31 popped from heap
22 13 3 1 31 40 52 77 98 100
v after 22 popped from heap
13 1 3 22 31 40 52 77 98 100
v after 13 popped from heap
3 1 13 22 31 40 52 77 98 100
v after 3 popped from heap
1 3 13 22 31 40 52 77 98 100
v after 1 popped from heap
1 3 13 22 31 40 52 77 98 100
```

Fig. 16.12 | Algorithms push_heap, pop_heap, make_heap and sort_heap. (Part 3 of 3.)

# ***make_heap*** Algorithm

Line 20 uses the **make_heap** algorithm to take a sequence of values in the range from a.begin() up to, but not including, a.end() and create a heap that can be used to produce a sorted sequence. The two iterator arguments must be *random-access iterators*, so this algorithm will work only with arrays, vectors and deques. A second version of this algorithm takes as a third argument a *binary predicate function for comparing values*.

# ***sort_heap*** Algorithm

Line 24 uses the **sort_heap** algorithm to sort a sequence of values in the range from a.begin() up to, but not including, a.end() that are already arranged in a heap. The two iterator arguments must be *random-access iterators*. A second version of this algorithm takes as a third argument a *binary predicate function for comparing values*.