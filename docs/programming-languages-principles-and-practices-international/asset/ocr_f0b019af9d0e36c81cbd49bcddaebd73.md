The process of exiting back through function calls to the caller during the search for a handler is called **call unwinding** or **stack unwinding**, the stack being the call stack whose structure is described in detail in the next chapter.

Once a handler has been found and executed, there remains the question of where to continue execution. One choice is to return to the point at which the exception was first raised and begin execution again with that statement or expression. This is called the **resumption model** of exception handling, and it requires that, during the search for a handler and possible call unwinding, the original environment and call structure must be preserved and reestablished prior to the resumption of execution.

The alternative to the resumption model is to continue execution with the code immediately following the block or expression in which the handler that is executed was found. This is called the **termination model** of exception handling, since it essentially discards all the unwound calls and blocks until a handler is found.

Virtually all modern languages, including C++, ML, and Ada, use the termination model of exception handling. The reasons are not obvious, but experience has shown that termination is easier to implement and fits better into structured programming techniques, while resumption is rarely needed and can be sufficiently simulated by the termination model when it is needed.

Here is an example of how to simulate the resumption model using termination in C++. Suppose that a call to new failed because there was not enough free memory left, and we wished to call a garbage collector and then try again. We could write the code as follows:

```
while (true)
    try
    { x = new X; // try to allocate
      break; // if we get here, success!
    }
    catch (bad_alloc)
    { collect_garbage(); // can't exit yet!
      if ( /* still not enough memory */ )
        // must give up to avoid infinite loop
      throw bad_alloc;
    }
```

Finally, we mention also that exception handling often carries substantial runtime overhead (see the next chapter for details). For that reason, and also because exceptions represent a not very structured control alternative, we want to avoid overusing exceptions to implement ordinary control situations, where simple tests would do the job. For example, given a binary search tree data structure (containing, e.g., integers), such as

```
struct Tree{
    int data;
    Tree * left;
    Tree * right;
};
```