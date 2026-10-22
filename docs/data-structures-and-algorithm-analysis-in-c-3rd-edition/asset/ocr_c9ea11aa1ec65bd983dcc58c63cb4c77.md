| Sort | 10 | 100 | 1K | 10K | 100K | 1M | Up | Down |
|---|---|---|---|---|---|---|---|---|
| Insertion | .00023 | .007 | 0.66 | 64.98 | 7381.0 | 674420 | 0.04 | 129.05 |
| Bubble | .00035 | .020 | 2.25 | 277.94 | 27691.0 | 2820680 | 70.64 | 108.69 |
| Selection | .00039 | .012 | 0.69 | 72.47 | 7356.0 | 780000 | 69.76 | 69.58 |
| Shell | .00034 | .008 | 0.14 | 1.99 | 30.2 | 554 | 0.44 | 0.79 |
| Shell/O | .00034 | .008 | 0.12 | 1.91 | 29.0 | 530 | 0.36 | 0.64 |
| Merge | .00050 | .010 | 0.12 | 1.61 | 19.3 | 219 | 0.83 | 0.79 |
| Merge/O | .00024 | .007 | 0.10 | 1.31 | 17.2 | 197 | 0.47 | 0.66 |
| Quick | .00048 | .008 | 0.11 | 1.37 | 15.7 | 162 | 0.37 | 0.40 |
| Quick/O | .00031 | .006 | 0.09 | 1.14 | 13.6 | 143 | 0.32 | 0.36 |
| Heap | .00050 | .011 | 0.16 | 2.08 | 26.7 | 391 | 1.57 | 1.56 |
| Heap/O | .00033 | .007 | 0.11 | 1.61 | 20.8 | 334 | 1.01 | 1.04 |
| Radix/4 | .00838 | .081 | 0.79 | 7.99 | 79.9 | 808 | 7.97 | 7.97 |
| Radix/8 | .00799 | .044 | 0.40 | 3.99 | 40.0 | 404 | 4.00 | 3.99 |

# Figure 7.20 Empirical comparison of sorting algorithms run on a 3.4-GHz Intel Pentium 4 CPU running Linux. Shellsort, Quicksort, Mergesort, and Heapsort each are shown with regular and optimized versions. Radix Sort is shown for 4- and 8-bit-per-pass versions. All times shown are milliseconds.

Figure 7.20 shows timing results for actual implementations of the sorting algorithms presented in this chapter. The algorithms compared include Insertion Sort, Bubble Sort, Selection Sort, Shellsort, Quicksort, Mergesort, Heapsort and Radix Sort. Shellsort shows both the basic version from Section 7.3 and another with increments based on division by three. Mergesort shows both the basic implementation from Section 7.4 and the optimized version (including calls to Insertion Sort for lists of length below nine). For Quicksort, two versions are compared: the basic implementation from Section 7.5 and an optimized version that does not partition sublists below length nine (with Insertion Sort performed at the end). The first Heapsort version uses the class definitions from Section 5.5. The second version removes all the class definitions and operates directly on the array using inlined code for all access functions.

Except for the rightmost columns, the input to each algorithm is a random array of integers. This affects the timing for some of the sorting algorithms. For example, Selection Sort is not being used to best advantage because the record size is small, so it does not get the best possible showing. The Radix Sort implementation certainly takes advantage of this key range in that it does not look at more digits than necessary. On the other hand, it was not optimized to use bit shifting instead of division, even though the bases used would permit this.

The various sorting algorithms are shown for lists of sizes 10, 100, 1000, 10,000, 100,000, and 1,000,000. The final two columns of each table show the performance for the algorithms on inputs of size 10,000 where the numbers are in ascending (sorted) and descending (reverse sorted) order, respectively. These columns demonstrate best-case performance for some algorithms and worst-case