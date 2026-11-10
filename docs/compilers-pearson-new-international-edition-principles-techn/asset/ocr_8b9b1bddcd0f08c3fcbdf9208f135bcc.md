# ### 7.6.6  Comparing Costs

Cheney’s algorithm has the advantage that it does not touch any of the unreachable objects. On the other hand, a copying garbage collector must move the contents of all the reachable objects. This process is especially expensive for large objects and for long-lived objects that survive multiple rounds of garbage collection. We can summarize the running time of each of the four algorithms described in this section, as follows. Each estimate ignores the cost of processing the root set.

+   - *Basic Mark-and-Sweep* (Algorithm 7.12): Proportional to the number of chunks in the heap.
+   - *Baker’s Mark-and-Sweep* (Algorithm 7.14): Proportional to the number of reached objects.
+   - *Basic Mark-and-Compact* (Algorithm 7.15): Proportional to the number of chunks in the heap plus the total size of the reached objects.
+   - *Cheney’s Copying Collector* (Algorithm 7.16): Proportional to the total size of the reached objects.

# ### 7.6.7  Exercises for Section 7.6

**Exercise 7.6.1:** Show the steps of a mark-and-sweep garbage collector on

+   a) Fig. 7.19 with the pointer *A* → *B* deleted.
+   b) Fig. 7.19 with the pointer *A* → *C* deleted.
+   c) Fig. 7.20 with the pointer *A* → *D* deleted.
+   d) Fig. 7.20 with the object *B* deleted.

**Exercise 7.6.2:** The Baker mark-and-sweep algorithm moves objects among four lists: *Free*, *Unreached*, *Unscanned*, and *Scanned*. For each of the object networks of Exercise 7.6.1, indicate for each object the sequence of lists on which it finds itself from just before garbage collection begins until just after it finishes.

**Exercise 7.6.3:** Suppose we perform a mark-and-compact garbage collection on each of the networks of Exercise 7.6.1. Also, suppose that

+   i. Each object has size 100 bytes, and
+   
+   ii. Initially, the nine objects in the heap are arranged in alphabetical order, starting at byte 0 of the heap.

What is the address of each object after garbage collection?