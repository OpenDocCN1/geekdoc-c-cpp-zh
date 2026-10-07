# SEMAPHORES

```
sem_t s;

void *child(void *arg) {
    printf("child\n");
    sem_post(&s); // signal here: child is done
    return NULL;
}

int main(int argc, char *argv[]) {
    sem_init(&s, 0, X); // what should X be?
    printf("begin\n");
    pthread_t c;
    pthread_create(&c, child, NULL);
    sem_wait(&s); // wait for child
    printf("end\n");
    return 0;
}
```

![](bbox=[0.268, 0.403, 0.663, 0.417])

so it can delete an element from it. In this pattern of usage, we often find one thread waiting for something, and another thread making that something happens and signaling that it has happened, waking the thread. We are thus using the semaphore as an ordering primitive (similar to our use of condition variables earlier).

A simple example is as follows. Imagine a parent creates another thread and then waits for it to complete its execution (Figure 31.6). When this program runs, we would like to see the following:

parent: begin
child
parent: end

The question is, how to use a semaphore to achieve this effect; as it turns out, the answer is relatively easy to understand. As you can see in the code, the parent calls sem_wait() and the child sem_post() to wait for the condition of the child finishing execution to become true. However, this raises the question: what should be the initial value of this semaphore?

(Again, think about it, instead of reading ahead)
The answer of course, is that the value of the semaphore should be set to 0. There are two cases to consider. First, let us assume that the parent creates the child but the child has not run yet (i.e., it is sitting in a waiting queue but not running). In this case (Figure 31.7, page 394), the parent will call sem_wait() before the child has called sem_post(); we'd like the parent to wait for the child to run. The only way this will happen is if the value of the semaphore is not greater than 0; hence, 0 is the initial value. The parent runs, decrements the semaphore (to -1), then waits (sleeping). When the child finally runs, it will call sem_post(), incre...