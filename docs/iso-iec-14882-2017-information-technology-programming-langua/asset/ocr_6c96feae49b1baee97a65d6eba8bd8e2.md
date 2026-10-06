It is implementation-defined whether the implementation-created execution of executes main(6.6.1) and the threads of execution created by std::thread(33.3.2) provides concurrent forward progress guarantees. [Note: General-purpose implementations provide these guarantees. — end note]

For a thread of execution calling forward progress guarantees, the implementation is not required to ensure that it will eventually make progress if it has not executed any execution step; if it has executed a step, it provides concurrent forward progress guarantees.

[Note: This does not specify a requirement for when to start this thread of execution, which will typically be specified by the entity that creates this thread of execution. For example, a thread of execution that provides concurrent forward progress guarantees and executes a task of tasks in an arbitrary order, one other, satisfies the requirements of forward progress for these tasks. — end note]

For a thread of execution weakly forward progress guarantees, the implementation does not ensure that it will eventually make progress.

[Note: Threads of execution weakly forward progress guarantees cannot be expected to make progress regardless of whether others make progress or not; however, with blocking forward delegation below, we can ensure that such threads of execution make progress eventually. — end note]

Concurrent forward progress guarantees are stronger than parallel forward progress guarantees, which are stronger than weakly parallel guarantees. For example, some kinds of synchronization between threads of execution may only make progress if the respective threads of execution provide forward progress guarantees, but fail to make progress under weakly parallel guarantees. — end note]

When a thread of execution P is specified with forward progress guarantee on the completion of a set S, then with forward thread of P being on S, the implementation shall ensure that the forward progress guarantees provided by at least one thread of execution in S at least as strong as P's forward progress guarantees. [Note: It is specified which thread or threads of execution are chosen and for which number of execution steps. The strengthening is not required and necessarily in place for the lifetime of the affected thread of execution. As long as P is blocked, the implementation has to ideally select and strengthen a thread of execution in S. Once S is empty, P is unblocked. — note]

[Note: A thread of execution B can temporarily provide an effectively stronger forward progress guarantee for a certain amount of time, due to another thread of execution A being blocked on B with forward progress delegation. If B then blocks on delegation to C, this may also provide a stronger forward progress guarantee to C. — end note]

[Note: If all threads of execution in S finishing (e.g., they terminate and do not use synchronization independently), P's execution of an operation that blocks with forward progress guarantee will not result in P's progress guarantee being weakened. — end note]

[Note: This does not remove any constraints regarding blocking synchronization for threads of execution providing parallel or weakly forward progress guarantees because the implementation is not required to strengthen a particular thread of execution whose-weak progress guarantee is preventing overall progress. — end note]

An implementation should ensure that the last value (in modification order) assigned by an atomic or synchronization operation become visible to all other threads in a finite period of time.

# 4.8 Acknowledgments

The C++ programming language described in this document is based on the language as described in Chapter R (Reference Manual) of Stroustrup. The C++ Programming Language (second edition, Addison-Wesley Publishing Company, ISBN 0-201-53992-6, ©1991 AT&T). That, in turn, is based on the