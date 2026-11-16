```
/*
 * Tests the execution speed of a given search function on a
 * vector.
 * search - the search function to test
 * v - the vector to search
 * trials - the number of trial runs to average
 * Returns the elapsed time in seconds
 * The C++ chrono library defines the types
 * system_clock::time_point and microseconds.
 */
double time_execution(int (*search)(const std::vector<int>&, int),
                      std::vector<int>& v, int trials) {
    int n = v.size();
    // Average the time over a specified number of trials
    double elapsed = 0.0;
    for (int iters = 0; iters < trials; iters++) {
        clock_t start_time = clock(); // Start the timer
        for (int i = 0; i < n; i++) {
            search(v, i); // Search for all elements
        }
        clock_t end_time = clock(); // Stop the timer
        elapsed += static_cast<double>(end_time - start_time)/CLOCKS_PER_SEC;
    }
    return elapsed/trials; // Mean elapsed time per run
}

int main() {
    std::cout << "\n-----------------------------------\n";
    std::cout << " Vector Linear Binary\n";
    std::cout << " Size Search Search\n";
    std::cout << "-----------------------------------\n";

    // Test the sorts on vectors with 1,000 elements up to
    // 10,000 elements.
    for (int size = 0; size <= 50000; size += 5000) {
        std::vector<int> list(size); // Make a vector of the appropriate size

        // Ensure the elements are ordered low to high
        for (int i = 0; i < size; i++) {
            list[i] = i;
        }

        std::cout << std::setw(7) << size;
        // Search for all the elements in list using linear search
        // Compute running time averaged over five runs
        std::cout << std::fixed << std::setprecision(3) << std::setw(12)
                  << time_execution(linear_search, list, 5)
                  << " sec";
        // Search for all the elements in list binary search
        // Compute running time averaged over 25 runs
        std::cout << std::fixed << std::setprecision(3) << std::setw(12)
                  << time_execution(binary_search, list, 25)
                  << " sec\n";
    }
}
```