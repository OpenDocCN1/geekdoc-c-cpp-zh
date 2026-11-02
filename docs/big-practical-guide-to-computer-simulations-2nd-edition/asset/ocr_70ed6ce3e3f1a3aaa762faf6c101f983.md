![](bbox=[0.18, 0.09, 0.88, 0.47])

Fig. 6.23 Number 15 is deleted from the heap shown in Fig. 6.22. First, number 15 replaced by the last element in the heap, number 33. Since at least one of the elements located at children is smaller, number 33 starts moving towards the leaves.

much faster simulation compared to the simple approach, hence much larger systems can be treated. A recent example is the study of heat conduction in one-dimensional systems of hard particles [Grassberger et al. (2002)], where the use of heaps led to qualitatively improved results compared to previous work [Dhar (2001)], where the simple approach had been applied.

Note that performing a simulation via collision events is not only possible for real hard particles but also for atoms with very short-ranged interactions, in this case one speaks of binary-collision approximation, which has been applied successfully for the simulations of ion impacts on surfaces in molecular-beam epitaxy [Robinson and Torrens (1974)].

In general, heaps can be applied widely. Whenever you have to select “the smallest” or “the largest” from a set of elements, you should always use a priority queue, e.g., implemented as a heap. Similar to the case of lists, in many cases you do not have to implement your own general-purpose priority queue, since it is already contained in the Standard Template Library, see Sec. 7.2. Nevertheless, in case you need double bookkeeping for highest performance, you have to have access to the internal heap structure. In this case you have to implement a heap yourself.

Nevertheless, before you change a part of your program and replace some simple selection mechanism by a heap-based selection, you should use gprof to analyze where your program spends most of its running time, see Sec. 4.4. Maybe the bulk of running time of your program is spent somewhere else. In this case you should optimize these parts first.