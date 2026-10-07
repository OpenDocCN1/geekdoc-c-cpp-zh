
## 28.5 Controlling Interrupts

One of the earliest solutions to provide mutual exclusion is to disable interrupts for critical sections; this solution was invented for single-processor systems. The code would look like this:

```c
void lock() {
    DisableInterrupts();
}
void unlock() {
    EnableInterrupts();
}
```

Assume we are running on a single-processor system. By turning off interrupts (using some kind of hardware instruction) before entering the critical section, we ensure that the critical section will not be interrupted, and will execute as if it were atomic. When we are finished, we re-enable interrupts (again, via a hardware instruction) and the program proceeds as usual.

The main positive of this approach is its simplicity. You certainly do not have to scratch your head to figure out how this works. Without interruption, a thread can be sure that the code executes and that no other thread will interfere with it.

The negatives, unfortunately, are many. First, this approach requires us to allow any calling thread to perform a privileged operation (turning interrupts on and off), and thus trust that this facility is not abused. As you already know, anyone is required to trust an arbitrary program; here, the trouble manifests in numerous ways: a greedy program could call lock() at the beginning of its execution and go into an endless loop. In this case, the OS or some malicious program could call lock() and never regains control of the system, and there is only one recourse: restart the system. Using interrupt disabling as a general-purpose synchronization solution requires too much in applications.

The second approach does not work on multiprocessors. If multiple threads are running on different CPUs, and each tries to enter the critical section, it does not matter whether interrupts are disabled; threads will be able to run on other processors, and thus could enter the critical section. As multiprocessors are now commonplace, so our general solution will have no better to do than this.

Third, turning off interrupts for extended periods of time can lead to interrupts becoming costly, which can lead to serious systems problems. For example, if the CPU missed the fact that a disk device has a finished read request, how will the OS know to process the waiting process for read?

Finally, and probably least important, this approach can be inefficient. Compared to normal instruction execution, code that masks or unmasks interrupts tends to be executed slowly by modern CPUs.

## LOCKS 335

```c
typedef struct __lock_t { int flag; } lock_t;

void init(lock_t *mutex) {
    // 0 -> lock is available, 1 -> held
    mutex->flag = 0;
}

void lock(lock_t *mutex) {
    while (mutex->flag == 1) // TEST the flag
        // spin-wait (do nothing)
    mutex->flag = 1; // now SET it!
}

void unlock(lock_t *mutex) {
    mutex->flag = 0;
}
```

> Figure 28.1: First Attempt: A Simple Flag

For reasons, turning off interrupts is only used in limited contexts as a mutual-exclusive primitive. For example, in some cases an operating system itself will use interrupt to guarantee atomicity when accessing its own data structures, or at least to prevent interrupt handling situations from arising. This usage makes sense, as the trust issue disappears the OS, which always trusts itself to perform privileged operations.

## 28.6 A Failed Attempt: Using Loads/Stores

To move beyond interrupt-based techniques, we will have to rely on CPU hardware and the instructions it provides to build a proper lock. Let's try to build a simple lock by using a simple variable. In this failed attempt, we'll see some of the basics needed to build a lock, and (hopefully) why just using a single variable and accessing it via normal loads and stores is insufficient.

In this first attempt (Figure 28), the idea is to use a simple variable (flag) to indicate whether the critical section has possession of a lock. The first thread that enters the critical section will call lock(), tests whether the flag is equal to 1 (in this case, it is not), and then sets the flag to 1 to indicate that the thread holds the lock. When finished with the critical section, the thread calls unlock() and clears the flag, indicating that the lock is no longer held.

If another thread tries to call lock() while first thread is in the critical section, it will simply spin-wait in the while loop for that to call unlock() and clear the flag. Once that first thread does so, the waiting thread will fall out of the while loop, set the flag to 1 for itself, and proceed into the critical section.

Unfortunately, the code has two problems: one of correctness, and another of performance.

© 2008–19, ARPACI-DUSSEAU THREE EASY PIECES

| Thread 1 | Thread 2 |
| :--- | :--- |
| `call lock()` | `call lock()` |
| `while (flag == 1)` | `while (flag == 1)` |
| `interrupt: switch to Thread 2` | `flag = 1; // set flag to 1 (too!)` |
| | `interrupt: switch to Thread 1` |
| | | 

The correctness problem is simple to see once you get to thinking about concurrent programming. Imagine the code interleaving in Figure 28.2; assume flag=0 to begin. 

As you can see from this interleaving, with timely (untimely?) interrupts, we can easily produce a case where both threads set the flag to 1 and both threads are able to switch the critical section. This behavior is what professionals call “bad” – we have obviously failed to provide the most basic requirement: providing mutual exclusion.

The performance problem, which we will address later on, is the fact that a thread waits to acquire a lock that is already held: it effectively checks the value of a lock, a technique known as spin-waiting. Spin-waiting wastes time for another thread to release the lock. The waste is exceptionally expensive on a uniprocessor, where the thread that is waiting cannot even run (at least, until a context switch occurs!) As we move forward and develop more sophisticated solutions, we should also consider.

## 28.7 Building Working Spin Locks with Test-And-Set

Because interrupts does not work on multiple processors (as shown above) and simple approaches using locks and stores (as above) do not work, designers wanted to invent hardware support for locking. The earliest multiprocessor systems, such as the Burroughs B85000 in the early 1960s (M82), had support; today all systems provide this type of support, for single CPU systems.

The simplest of hardware support is known as a test-and-set (or atomic exchange) instruction. We define what the test-and-set instruction does using the following C snippet:

```c
int testAndSet(int *old_ptr, int new) {
    int old = *old_ptr; // fetch old value at old_ptr
    *old_ptr = new; // store 'new' into old_ptr
    return old; // return the old value
}
```

> Each architecture that supports test-and-set has a different name. On SPARC it is the load/store unsigned by byte (ldstub) on x86 it is the locked version of the atomic exchange (xchg).

## LOCKS

## ASIDE: DEKKER’S AND PETERSON’S ALGORITHMS

In the 1960s, Dijkstra posed the concurrency problem to his friends, and one of them, a mathematician named Theodorus Jozef Dekker, came with a solution [D68]. Unlike the solutions we discuss here, which use special hardware instructions and ever OS support, Dekker's algorithm uses just loads and stores (assuming they are atomic with respect to each other, which was true on early hardware).

Dekker's approach was later refined by Peterson [P81]. Once again, just loads and stores are used, and the idea is to ensure that two threads never enter a critical section at the same time. Here is Peterson's algorithm (for two threads); see if you can understand the code. What are the flag and turn variables used?

```c
int flag[2];
int turn;

void init() {
    // indicate you intend to hold the lock w/ 'flag'
    flag[0] = 0;
    // whose turn is it? (thread 0 or 1)
    turn = 0;
}

void lock() {
    // 'self' is the thread ID of caller
    flag[self] = 1;
    // make it other thread's turn
    turn = 1 - self;
    while ((flag[1-self]) == 1) && (turn == 1 - self)) {
        // spin-wait while it's not your turn
    }
}
void unlock() {
    // simply undo your intent
    flag[self] = 0;
}
```

For some reason, developing locks that work without special hardware support became all for a while, giving theory-types a lot of problems to work on. Of course, this line of work became quite useless unless realized it is much easier to assume a little hardware support (and indeed support had been around from the earliest days of multipcessing). Further, algorithms like the ones above dont work on modern hardware (due to relaxed memory consistency models), making them even less useful than they were before. More research relegated to the dustbin of history...
