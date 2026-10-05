# 10.5. MAKING FUNCTIONS stop_time REUSABLE

```
clock_t stop_time = clock(); // Record stop time
running = false; // Stop the clock
// Add to the elapsed time how long it has been since we last
// started the timer
elapsed += static_cast<double>((stop_time - start_time)
// CLOCKS_PER_SEC);
}

// Return the cumulative running time (in seconds)
// kept by the timer since it was reset
double elapsed_time() {
    if (running) { // Compute time since last reset
        clock_t current_time = clock(); // Record current time
        return elapsed + static_cast<double>(current_time - start_time)
        // CLOCKS_PER_SEC);
    } else {
        // Timer stopped; elapsed already computed in stop_timer
        return elapsed;
    }
}
```

Observe that the code in Listing 10.13 (timodule.cpp) allows client to store the timer and restart it without losing any previously accumulated. The implementation uses three global variables—elapsed, start_timer, and running—to maintain the state of the timer. One or more of these global variables are influenced by three functions—start_timer, stop_timer, reset_time. The fourth returns the value of the elapsed variable.

Listing 10.14 (bettertime.cpp) simplifies Listing 8.7 (timeit.cpp) with our new timer module.

# Listing 10.14 bettertime.cpp

```
#include <iostream>
#include "timodule.h" // Out timer module

using namespace std;

int main() {
    char letter;
    cout << "Enter a character: "; // Start timing
    start_timer();
    cin >> letter;
    stop_timer(); // Stop timing
    cout << elapsed_time() << " seconds" << endl;
}
```

The code within Listing 10.14 (bettertime.cpp) is simpler than the code in Listing 8.7 (timeit.cpp). All traces of the clock_t time and the memory arithmetic and casting are gone. The timer provides a simple interface to callers that hides the details on how the timing actually happens.

Despite the use of our timer module, it has a severe limitation. Suppose you want to measure how long it takes for a function to execute and also, during function's execution, separately a time a smaller section of code within that function. When the function is finished executing, you would like to know how long it took to do its job and how long portion of its code to execute. We would essentially need two independent timers, but with our timer it is not possible to code simultaneously more than one. We will see a far superior way to program an execution timer in