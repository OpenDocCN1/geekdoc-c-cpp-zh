# CONCURRENCY: AN INTRODUCTION

```
#include <stdio.h>
#include <thread.h>
#include <common.h>
#include <common_threads.h>
static volatile int counter = 0;

// mythread())
// Simply adds 1 to counter repeatedly, in a loop
// No, this is not how you would add 10,000 to
// a counter, but it also shows the problem nicely.

void mythread(void *arg) {
    printf("%s: begin\n", (char *) arg);
    int i;
    for (i = 0; i < le7; i++) {
        counter = counter + 1;
    }
    printf("%s: done\n", (char *) arg);
    return NULL;
}

void main () {
// Just launches two threads (pthread_create)
// and then waits for them (pthread_join)

int main(int argc, char *argv[]) {
    printf("main: begin (counter = %d\n", counter);
    pthread_create(&p1, NULL, mythread, "A");
    pthread_create(&p2, NULL, mythread, "B");

// join waits for the threads to finish
    pthread_join(p1, NULL);
    pthread_join(p2, NULL);
    printf("main: done with both (counter = %d\n", counter);
    return 0;
}
```

Figure 26.6: Sharing Data: Uh Oh (t1.c)