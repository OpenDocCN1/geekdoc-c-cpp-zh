# CONDITION VARIABLES

```
// how many bytes of the heap are free?
int bytesLeft = MAX_HEAP_SIZE;

// need lock and condition too
cond_t c;
mutex_t m;

void *ptr =
allocate(int size) {
    Pthread_mutex_lock(&m);
    while (bytesLeft < size) {
        Pthread_cond_wait(&c, &m); // get mem from heap
    bytesLeft -= size;
    Pthread_mutex_unlock(&m);
    return ptr;
}

void free(void *ptr, int size) {
    Pthread_mutex_lock(&m);
    bytesLeft += size;
    Pthread_cond_signal(&c); // whom to signal??
    Pthread_mutex_unlock(&m);
}
```

Figure 30.15: Covering Conditions: An Example

Consider the following scenario. Assume there are zero bytes free; T1 calls allocate(100), followed by T2 which asks for less memory by calling allocate(10). Both T1 and T2 will wait on the condition and to sleep; there are not enough bytes to satisfy either of these requests.

At that point, assume a third thread, T3, calls free(50). Unfortunately, when it calls while waiting for a waking thread, it might not wake the correct thread, T2 is waiting for only 10 bytes to be free; T3 should remain waiting, as not enough memory is yet free. The code in the figure does not work, as the waking other threads do not know which thread (or threads) to wake up.

The solution suggested by Lampson and Redell is straightforward: replace pthread_signal with pthread_broadcast which wakes up all waiting threads. By doing so, we guarantee that any threads that should be woken are. The downside, of course, can be a negative performance impact, as we might needlessly wake up many other threads that shouldn't (yet) be awake. Those threads will simply wake up, re-check the condition, and then immediately go back to sleep.

Lampson and Redell call such a condition covering condition, as it covers all the cases where a thread needs to wake up (conservatively); the cost, as we've discussed, is that too many threads might be woken.