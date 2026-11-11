The call `newNode->next = head.load()` loads the old value of head. If the loaded value `newNode->next` is still the same as head in line 23, head is updated to the `newNode` and the call `head.compare_exchange_strong` returns true. If not, the call returns false and the while loop is executed until the call returns true. `head.compare_exchange_strong` returns false if another thread added in the meantime a new node to the stack. When you apply `compare_exchange_strong` in a loop, you can also use `compare_exchange_weak`. `compare_exchange_weak` can spuriously fail and return false if head is equal to `newNode->next`. Due to the recursion, this would cause only an additional iteration.

Lines 22 and 23 build a kind of atomic transaction. First, you make a snapshot of the data structure (line 22), then you try to publish the transaction (line 23). If the snapshot is not valid anymore, you make a rollback and try it once more.

> > **push is lock-free but not wait-free**
> >
> > The previous implementation of the member function push is lock-free but not wait-free. When many threads call `compare_exchange_strong` concurrently, only one thread can make progress. All other threads have to wait.

The simplified version has two issues. First, it does not have a pull operation, and second, it releases no memory. I address both issues in the next implementation.

# ## 14.2.2 A Complete Implementation

Typically, a stack supports the member functions push, pop, and top. Implementing the pop and top member functions thread-safe, does not guarantee that the invocation of top followed by pop is thread-safe. It may happen that one thread t1 called `stack.top()` and is interleaved by another thread t2 that called `stack.top()` and then `stack.pop()`. Now, the final `t1.pop()` call is based on the wrong stack size. Read more about this issue in the previous chapter about the concurrent stack.

# ### 14.2.2.1 No Memory Reclamation

Consequently, the following implementation combines both member functions top and pop into one: `topAndPop`.