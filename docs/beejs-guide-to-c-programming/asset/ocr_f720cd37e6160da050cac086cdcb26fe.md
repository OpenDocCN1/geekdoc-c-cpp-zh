```
printf("Thread: is awake\n");

 t = 0;

// Add everything up
for (int i = 0; i < VALUE_COUNT_MAX; i++)
    t += value[i];

printf("Thread: total is %d\n", t);

// Reset input index for main thread
value_count = 0;

mtx_unlock(&value_mtx); // <-- MUTEX UNLOCK
}

return 0;

int main(void)
{
    thrd_t t;

    // Spawn a new thread
thrd_create(&t, run, NULL);
thrd_detach(&t);

    // Set up the mutex and condition variable

mtx_init(&value_mtx, mtx_plain);
cnd_init(&value_cnd);

for (;;) {
    int n;
    scanf("%d", &n);

    mtx_lock(&value_mtx); // <-- LOCK MUTEX
    value_count++ = n;

    if (value_count == VALUE_COUNT_MAX) {
        printf("Main: signaling thread\n");
cnd_signal(&value_cnd); // <-- SIGNAL CONDITION
    }

    mtx_unlock(&value_mtx); // <-- UNLOCK MUTEX
}

// Clean up (I know that's an infinite loop above here, but I
// want to at least least pretend to be proper);
```