
# LOCK-BASED CONCURRENT DATA STRUCTURES

```c
typedef struct __node_t {
    int             value;
    struct __node_t *next;
} node_t;
```

```c
typedef struct __queue_t {
    node_t              head;
    node_t              tail;
    pthread_mutex_t head_lock, tail_lock;
} queue_t;
```

```c
void Queue_Init(queue_t *q) {
    node_t *tmp = malloc(sizeof(node_t));
    tmp->next = NULL;
    q->head = q->tail = tmp;
    pthread_mutex_init(&q->head_lock, NULL);
    pthread_mutex_init(&q->tail_lock, NULL);
}
```

```c
void Queue_Enqueue(queue_t *q, int value) {
    node_t *tmp = malloc(sizeof(node_t));
    assert(tmp != NULL);
    tmp->value = value;
    tmp->next = NULL;

    pthread_mutex_lock(&q->tail_lock);
    q->tail->next = tmp;
    q->tail = tmp;
    pthread_mutex_unlock(&q->tail_lock);
}
```

```c
int Queue_Dequeue(queue_t *q, int *value) {
    pthread_mutex_lock(&q->head_lock);
    node_t *tmp = q->head;
    node_t *new_head = tmp->next;
    if (new_head == NULL) {
        pthread_mutex_unlock(&q->head_lock);
        return -1; // queue is empty
    }
    *value = new_head->value;
    q->head = new_head;
    pthread_mutex_unlock(&q->head_lock);
    free(tmp);
    return 0;
}
```

Figure 29.9: Michael and Scott Concurrent Queue

```c
#define BUCKETS (101)
struct __hash_t {
    list_t lists[BUCKETS];
} hash_t;

void Hash_Init(hash_t *H) {
    int i;
    for (i = 0; i < BUCKETS; i++) {
        List_Init(&H->lists[i]);
    }
}

int Hash_Insert(hash_t *H, int key) {
    List_Insert(&H->lists[key % BUCKETS], key);
}

int Hash_Lookup(hash_t *H, int key) {
    return List_Lookup(&H->lists[key % BUCKETS], key);
}
```

![](img/133d518e3f69fcaaead32c56ae6c49_0)

## 29.4 Concurrent Hash Table

We end our discussion with a simple and widely applicable concurrent structure, the hash table. We'll focus on a simple hash table that does not resize; little more work is required to handle resizing, which we leave as an exercise for the reader. This concurrent hash table (Figure 29.10) is straightforward, built using the lists we developed earlier, and works incredibly well. The reason for its good performance is that instead of having a single lock for the entire structure, it uses a lock per bucket (each of which is represented by a lock). Doing so enables many concurrent operations to take place.

Figure 29.11 shows the performance of the hash table under concurrent updates (from 10,000 to 50,000 updates from four threads, on four CPUs). Also, for the sake of comparison, the performance of a linked list (with a single lock) scales significantly; the hash table does not.

## 29.5 Summary

We have introduced sampling data structures, from counters to lists and queues, and finally to the ubiquitous hash table. We have learned a few important lessons along the way: to be careful with acquisition and release of locks around control flow; that enabling more concurrency does not necessarily increase performance; that performance should only be remedied once they exist. This last point, avoiding premature optimization, is central to any performance-minded developer; there is no value in making something faster than the application. Of course, we have just scratched the surface of high performance structures; see Michael's excellent survey for more information, as well as other sources. In particular, you might be interested in other structures (such as B-trees); for this knowledge, a database class is your best bet. You might also be interested in techniques that don't use locks at all; such non-blocking data structures are something we'll get a taste of in the chapter on concurrency bugs, but frankly this topic is an entire area requiring more study than possible. Find out more on your own if you are interested!

> TIP: AVOID PREMATURE OPTIMIZATION (KNUTH'S LAW). When building a concurrent data structure, start with the most basic approach, which is to add a single lock to provide synchronized access. By doing so, you are likely to build a correct lock; if you then find that it suffers from performance problems, you can refine it, thus making it fast if needed. As Knuth famously stated, "Premature optimization is the root of all evil." Many systems utilized a single lock when transitioning to multiprocessors, including Sun OS and Linux. In the latter, this lock had a name, the big kernel lock (BKL). For many years, this simple approach was good enough, until a single active thread in the kernel at a time became a bottleneck. Thus, it was finally time to add optimization of improved concurrency to these systems. Within Linux, the more straightforward approach was taken: replace one lock with many. Within Sun, a more radical decision was made: build a brand new operating system, known as Solaris, that incorporates concurrency fundamentally from day one. Read the Linux and Solaris kernel books for more information about these systems.

## References

- [B10] "Analysis of Linux Scalability to Many Cores" by Silas Boyd-Wickizer, Austin T. Devoshi, Yangdong Mao, Alexey Peseter, M. Franks Kaashok, Robert Morris, Nikolai Zedovich. A great study of how Linux performs on multicore machines, as well as some simple solutions. It needs a *sloppy* counter to solve one of the scaling problem contention.
- [BH73] "Operating Systems Principles" by Peter Hahn. Prentice-Hall, 1973. Available: http://portal.acm.org/citation.cfm=540365. One of the first books on operating systems ahead of its time. Introduced as a concurrency primitive.
- [BC05] "The Linux Kernel (Third Edition)" by Daniel P. Bovet and Marco Cesati. O'Reilly Media, 2005. The classic on the Linux kernel. You should read it.
- [C06] "The Search for Fast Cycles" by Jonathan Bonter. February 1, 2006. Available: http://lwn.net/Articles/170003. LWN has many wonderful articles about the latest in Linux. This article is a short description of approximate counting; read it, and others, to learn about the latest in Linux.
- [L13] "An Analysis of Linux File System Evolution" by Lance Lu, Andrea C. Arpaci-Dusseau, Remi H. Arpaci-Dusseau, Shan Lu. San Jose, CA, February 2013. Our study traces patches to Linux file systems over nearly a decade. Lots of finds there; read it to see! The work was painful to do; the poor graduate student, to look through every detail by hand.
- [M98] "Nonblocking Algorithms and Preemption-Safe Locking on Multiprocessed Shared-Memory Processors." M. Michael Scott. Journal of Parallel and Distributed Computing, Vol. 51, No. 1, 1998. Professor Scott and his students have been at the forefront of concurrency algorithms and data structures for many years; check out his web page, numerous papers, or to find out.
- [MS04] "Concurrent Data Structures" by Mok Nair and Sahni. Chapman and Hall/CRC Press, 2004. Available: www.cs.tsau.edu/shani/concurrent-data-structures.pdf. A short but comprehensive reference on concurrent data structures. Though it is missing some of the latest works in the field, it is an incredibly useful reference.
- [MM00] "Internals: Kernel Architecture" by Jim Mauro and Richard McDougall. Prentice Hall, October 2000. The Solaris book. But If you want to learn about something other than Linux.
- [S+11] "Making the Common Case the Only Case with Anticipatory Memory Allocation" by Sundarasan, Sundarasan, Jupu Zhang, Seiram Subramanianian, Andrea C. Arpaci-Dusseau, Remzi H. Arpaci-Dusseau. FAST '11, San Jose, CA, February 2011. Our work on removing possibly-failing allocation calls from kernel nodes. By allocating all potentially needed memory before doing any work, we avoid failure depth in the storage stack.
