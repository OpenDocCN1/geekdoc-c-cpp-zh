# SEMAPHORES

TIP: SIMPLE AND DUMB CAN BE BETTER (HILL’S LAW)
You should never underestimate the notion that the simple and dumb approach can be the best one. With locking, sometimes a simple spin lock works best, it is easy to implement and fast. Although something reader/writer locks sounds cool, they are complex, and can mean slow. Thus, always try the simple and dumb approach first.
This idea, appealing to simplicity, is found in many places. One early source is Mark Hill's dissertation [H87], which studied how to design caches for CPUs. Hill found that simple direct-mapped caches better than fancy set-associative designs (one reason is that in caching, designs enable faster lookups). As Hill succinctly summarized his work: "Big and dumb is better." And thus we call this similar advice Hill's Law.

# 31.6 The Dining Philosophers

One of the most famous problems posed, and solved, by Dijkstra, is known as the dining philosopher's problem [D71]. The problem is famous because it is fun and somewhat intellectually interesting; however, its practical utility is low. However, its false focus inclusion; indeed, you might be asked about it in some interview, and you'd really hate your OS professor if you miss that question and don't get the job. Conversely, if you get the job, feel free to send to your OS professor a nice note, or some options.
The basic setup for the problem is (as shown in Figure 31.14): as-there are five “philosophers” sitting around a table. Between each pair of philosophers is a single fork (and thus, total). The philosophers have times when they think, and don't need any forks, and when they eat. To eat, a philosopher needs two forks, the one on their left and the one on their right. The contention for forks, and synchronization problems that ensue, are what makes this problem we study in concurrent programming.
Here is the basic loop of each philosopher, assuming each has a unique identifier p from 0 to 4 (inclusive):

```
while (1) {
    think();
    get_forks(p);
    eat();
    put_forks(p);
}
```

The key challenge, then, is to write the routines get_forks() and put_forks() such that there is no deadlock, no philosopher starves and

© 2008–19, ARPACI-DUSSESEAU

THREE
EASY
PIECES