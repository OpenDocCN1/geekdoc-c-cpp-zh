Listing 16.5 (loggingflexiblesort.cpp) is a variation of Listing 12.2 (flexibleinsertsort.cpp) that uses a comparison object instead of a comparison_function.

# Listing 16.5: loggingflexiblesort.cpp

```
#include <iostream>
#include <vector>

/*
 * Comparer objects manage the comparisons and element
 * interchanges on the selection sort function below.
 */
class Comparer {
   // Keeps track of the number of comparisons
   // performed
   int compare_count;
   // Keeps track of the number of swaps performed
   int swap_count;
   // Function pointer directed to the function to
   // perform the comparison
   bool (*comp)(int, int);
public:
   // The client must initialize a Comparer object with a
   // suitable comparison function.
   Comparer(bool (*f)(int, int)) {
      compare_count(0), swap_count(0), comp(f) {}
   }

   // Resets the counters to make ready for a new sort
   void reset() {
      compare_count = swap_count = 0;
   }

   // Method that performs the comparison. It delegates
   // the actual work to the function pointed to by comp.
   // This method logs each invocation.
   bool compare(int m, int n) {
      compare_count++;
      return comp(m, n);
   }

   // Method that performs the swap.
   // Interchange the values of
   // its parameters a and b which are
   // passed by reference.
   // This method logs each invocation.
   void swap(int& m, int& n) {
      swap_count++;
      int temp = m;
      m = n;
      n = temp;
   }

   // Returns the number of comparisons this object has
   // performed since it was created.
   int comparisons() const {
```