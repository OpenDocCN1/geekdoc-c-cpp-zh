In this example, we will create two threads. Both will modify and access a thread-specific variable to demonstrate that changes made by one thread do not affect the other.

```
#include #include #include pthread_key_t key; pthread_once_t key_once
= PTHREAD_ONCE_INIT; void make_key() {
pthread_key_create(&key, NULL); } *ignored_argument) {
pthread_once(&key_once, make_key); *my_key_data = *
pthread_getpecific(key); (!my_key_data) { == 0; // Initialize to 0
pthread_setspecific(key, my_key_data); *my_key_data); NULL; } int {
threads[2]; i = 0; i < 2; ++i pthread_create(&threads[i], NULL,
thread_func, NULL); i = 0; i < 2; ++i pthread_join(threads[i], NULL); 0;
}
```

Thread 140101010109235264: 1
Thread 14010101019315968: 1

In this example, both threads increment their own instance of the my_key_data variable, demonstrating that the data they manipulate specific to each thread and do not interfere with each other.

# Best Practices for Using Thread-Specific

Initialization and Always initialize thread-specific data before use and include cleanup routines to release resources when no longer needed. Key Reuse thread-specific data keys whenever possible to limit resource consumption.