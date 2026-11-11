inside. From the outside means that it is in the responsibility of the caller (application) to protect the data. This outside perspective is the perspective I mainly used in this book until now. From inside means that the data structure is responsible for protecting itself. A data structure that protects itself so that no data race can appear is called thread-safe. This inside perspective is the perspective I write about in this and the next chapter.

First of all, what are the general consideration you have to keep in mind to design a concurrent data structure?

Implementing thread-safe data structures is special. Before I dive into each of these unique concerns, here is a concise overview, including the answers you have to give.

+   - **Locking Strategy:** Should the data structure support coarse-grained, fine-grained locking, or be lock-free? Coarse-grained locking might be easier to implement but introduces contention. A fine-grained implementation or a lock-free one is way more challenging.
+   - **The Granularity of the Interface:** The bigger the thread-safe data structure’s interface, the more difficult it becomes to reason about the concurrent usage of the data structure.
+   - **Typical Usage Pattern:** When readers use your data structure mainly, you should not optimize for writers.
+   - **Avoidance of Loopholes:** Don’t pass internals of your data structure to clients.
+   - **Contention:** Do concurrent client requests seldom or often use your data structure?
+   - **Scalability:** How is your data structure’s performance characteristic when the number of concurrent clients increases or the data structure is bounded?
+   - **Invariants:** Which invariant must hold for your data structure when used?
+   - **Exceptions:** What should happen if an exception occurs?

Of course, these considerations are dependent on each other. For example, using a coarse-grained locking strategy lets you think about the granularity of the interface and the invariants. In contrast, it may increase the contention on the data structure and breaks scalability.

Although the general considerations in this chapter apply to lock-based data structures and the lock-free data structures, most examples in this chapter use locks. I delay all detailed discussions about lock-free data structures to the dedicated chapter.

# 12.2 Locking Strategy

Should the data structure support coarse-grained, fine-grained locking or be lock-free? First of all, what do I mean by coarse-grained locking? Coarse-grained locking means that only one thread uses the data structure at one point in time. The thread-safe interface pattern when using one lock is a typical way to implement coarse-grained locking. Here is the straightforward idea of the thread-safe interface pattern.

+   - All interface member functions (`public`) should use a lock.