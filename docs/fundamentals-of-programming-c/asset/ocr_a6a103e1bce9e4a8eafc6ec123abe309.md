# 16.2. STOPWATCH

```
// Add time from previous elapsed to the current elapsed
// since the latest call to the start method.
    return elapsed_time
        + static_cast<double>((current_time - start_time))
        / CLOCKS_PER_SEC);
}
else {
    // Timer stopped; elapsed time already computed in the stop method
    return elapsed_time;
}

// Returns the stopwatch's status (running or not) to the client.
// This method does not affect the state of the stopwatch.
bool Stopwatch::is_running() const {
    return running;
}

// Resets the stopwatch so a subsequent start begins recording
// a new time Stops the stopwatch if it is currently running.
void Stopwatch::reset() {
    running = false;
    elapsed_time = 0.0;
}
```

Note that our design allows a client to see the running time of a Stopwatch object without needing to stop it. An alternate design might print an error message and perhaps exit the program's execution if a client attempts to see the elapsed time of a stopwatch.

Some aspects of the Stopwatch class are notable:

+   - Stopwatch uses three instance variables:
    - The start_time instance variable records the time when the client last called the start method.
    - The elapsed_time instance variable keeps track of the time since the last call to the reset method.
    - The running instance variable indicates whether or not the clock is running.

+   - The constructor sets the initial values of the instance variables start_time, elapsed_time, and running.
- The start method notes the system time after the assignment to running. If these two statements were reversed, the elapsed time would include the time to the assignment to running as close as possible just include the statements in the client code between the start and stop method calls.
Notice that start_time is not assigned if it is currently not zero. This allows a client to stop the stopwatch and restart it without losing any segment of time.
- In the stop method, the time is noted before the assignment to running so the elapsed time does not include the assignment to running. This provides a more accurate accounting of the client code execution time.
- The stop method computes the accumulated elapsed time.