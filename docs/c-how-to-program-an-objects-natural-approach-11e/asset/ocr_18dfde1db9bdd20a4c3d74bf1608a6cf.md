```
```text
Operation                  Buffer    Occupied
---------                  ------    --------
Producer writes 1          1         true
Consumer reads 1           1         false
Producer writes 2          2         true
Consumer reads 2           2         false
Producer writes 3          3         true
Consumer reads 3           3         false
Producer writes 4          4         true
Consumer reads 4           4         false
Producer writes 5          5         true
Consumer reads 5           5         false
Producer writes 6          6         true
Consumer reads 6           6         false
Producer writes 7          7         true
Consumer reads 7           7         false
Producer writes 8          8         true
Consumer reads 8           8         false
Producer writes 9          9         true
Consumer reads 9           9         false
Producer writes 10         10        true
Producer done producing
Terminating Producer
Consumer reads 10           10        false

Consumer read values totaling 55
Terminating Consumer
```
```

**Fig. 17.16** | *SynchronizedBuffer* using two `binary_semaphores` to maintain synchronized access to a shared mutable int. (Part 2 of 2.)

Figure 17.16 uses two `std::binary_semaphores` to coordinate the producer and consumer threads:

+   - `m_produce` (line 47) is initialized with the count 1, indicating that the producer initially can produce a value because `m_buffer` is empty.
+   - `m_consume` (line 48) is initialized with the count 0, indicating that the consumer initially cannot consume a value because `m_buffer` is empty.

This example uses `m_occupied` (line 49) for output purposes only—it does not play a role in this example’s thread synchronization.

# SynchronizedBuffer Member Function put

`SynchronizedBuffer`’s logic is simplified with `std::binary_semaphores`. When the producer thread calls `put` (defined at lines 15–27), line 17 calls `m_produce`’s acquire member function. If `m_produce`’s count is 0, the producer thread will be blocked until the count is 1. If the count is 1, the producer thread acquires the semaphore, decreasing its count to 0, and writes a new value into `m_buffer`. The producer cannot produce again until `m_produce`’s count is 1, which will occur only when the consumer consumes the buffer’s value.

When the producer is done updating the buffer, line 26 calls `m_consume`’s release member function to increment that semaphore’s count to 1. If a consumer thread is blocked waiting to acquire `m_consume`, it unlocks so it can proceed. Otherwise, when a consumer tries to call `get`, it can immediately acquire `m_consume` and proceed.