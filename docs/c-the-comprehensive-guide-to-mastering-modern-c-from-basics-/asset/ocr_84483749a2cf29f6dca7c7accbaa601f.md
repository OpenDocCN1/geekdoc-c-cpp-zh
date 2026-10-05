In swap, you need to lock the mutexes of both parameters to ensure that no other thread changes either parameter to an inconsistent state during the swap. Locking two mutexes means a risk of deadlock. The solution is this:

+   - First, lock both mutexes simultaneously with the function `lock(...)`.
- To ensure that the locks are automatically released, use `lock_guard`, but you must indicate with the additional parameter `adopt_lock` that the mutexes are already locked and do not need to be locked again in the `lock_guard` constructor.

As usual, `libre` and `lkli` release their locks again when leaving the critical section.

Here are the general notes on the listing: I implemented `swap` according to the usual idiom—namely, a `friend` function—so that it can be used as a free function like `swap(a,b)` instead of a method like `swap(b)`. This is the way the function best cooperates with the standard library. Within `swap`, you should first check, similar to assignment, `swap(a,a)` has been called directly or indirectly, making the swap unnecessary and perhaps even dangerous.

# Tips for Avoiding Deadlocks

It is difficult to completely avoid potential deadlocks. Nevertheless, it is essential to achieve this. Therefore, careful consideration and testing are important—and even more so because finding errors related to threads