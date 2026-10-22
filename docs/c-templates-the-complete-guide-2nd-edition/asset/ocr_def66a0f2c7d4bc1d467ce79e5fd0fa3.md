```
debugging/tracer.hpp

#include <iostream>

class SortTracer {
    private:
        int value;                      // integer value to be sorted
        int generation;                 // generation of this tracer
        inline static long n_created = 0;   // number of constructor calls
        inline static long n_destroyed = 0; // number of destructor calls
        inline static long n_assigned = 0;  // number of assignments
        inline static long n_compared = 0;  // number of comparisons
        inline static long n_max_live = 0;  // maximum of existing objects

        // recompute maximum of existing objects
        static void update_max_live() {
            if (n_created - n_destroyed > n_max_live) {
                n_max_live = n_created - n_destroyed;
            }
        }
}
```