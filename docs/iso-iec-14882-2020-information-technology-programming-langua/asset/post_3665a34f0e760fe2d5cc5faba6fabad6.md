
[Note 10: In the absence of consume operations, the happens before and simply happens before relations are identical. — end note]

## 12 An evaluation A strongly happens before an evaluation D if, either

- (12.1) — A is sequenced before D, or
- (12.2) — A synchronizes with D, and both A and D are sequentially consistent atomic operations (31.4), or
- (12.3) — there are evaluations B and C such that A is sequenced before B, B simply happens before C, and C is sequenced before D, or
- (12.4) — there is an evaluation B such that A strongly happens before B, and B strongly happens before D.

[Note 11: Informally, if A strongly happens before B, then A appears to be evaluated before B in all contexts. Strongly happens before excludes consume operations. — end note]

## 13 A visible side effect A on a scalar object or bit-field M with respect to a value computation B of M satisfies the conditions:

- (13.1) — A happens before B and
- (13.2) — there is no other side effect X to M such that A happens before X and X happens before B.

The value of a non-atomic scalar object or bit-field M, as determined by evaluation B, shall be the value stored by the visible side effect A.

[Note 12: If there is ambiguity about which side effect to a non-atomic object or bit-field is visible, then the behavior is either unspecified or undefined. — end note]

[Note 13: This states that operations on ordinary objects are not visibly reordered. This is not actually detectable without data races, but it is necessary to ensure that data races, as defined below, and with suitable restrictions on the use of atomics, correspond to data races in a simple interleaved (sequentially consistent) execution. — end note]

## 14 The value of an atomic object M, as determined by evaluation B, shall be the value stored by some side effect A that modifies M, where B does not happen before A.

[Note 14: The set of such side effects is also restricted by the rest of the rules described here, and in particular, by the coherence requirements below. — end note]

## 15 If an operation A that modifies an atomic object M happens before an operation B that modifies M, then A shall be earlier than B in the modification order of M.

[Note 15: This requirement is known as write-write coherence. — end note]

## 16 If a value computation A of an atomic object M happens before a value computation B of M, and A takes its value from a side effect X on M, then the value computed by B shall either be the value stored by X or the value stored by a side effect Y on M, where Y follows X in the modification order of M.

[Note 16: This requirement is known as read-read coherence. — end note]

## 17 If a value computation A of an atomic object M happens before an operation B that modifies M, then A shall take its value from a side effect X on M, where X precedes B in the modification order of M.

[Note 17: This requirement is known as read-write coherence. — end note]

## 18 If a side effect X on an atomic object M happens before a value computation B of M, then the evaluation B shall take its value from X or from a side effect Y that follows X in the modification order of M.

[Note 18: This requirement is known as write-read coherence. — end note]

## 19 [Note 19: The four preceding coherence requirements effectively disallow compiler reordering of atomic operations to a single object, even if both operations are relaxed loads. This effectively makes the cache coherence guarantee provided by most hardware available to C++ atomic operations. — end note]

## 20 [Note 20: The value observed by a load of an atomic depends on the "happens before" relation, which depends on the values observed by loads of atomics. The intended reading is that there must exist an association of atomic loads with modifications they observe that, together with suitably chosen modification orders and the "happens before" relation derived as described above, satisfy the resulting constraints as imposed here. — end note]

## 21 Two actions are potentially concurrent if

- (21.1) — they are performed by different threads, or
- (21.2) — they are unsequenced, at least one is performed by a signal handler, and they are not both performed by the same signal handler invocation.

## 4 An invocation of a standard library function that blocks (3.7) is considered to continuously execute execution steps while waiting for the condition that it blocks on to be satisfied.

[Example 1: A library I/O function that blocks until the I/O operation is complete can be considered to continuously check whether the operation is complete. Each such check consists of one or more execution steps, for example using observable behavior of the abstract machine. — end example]

## 5 [Note 4: Because of this and the preceding requirement regarding what threads of execution have to perform eventually, it follows that no thread of execution can execute forever without an execution step occurring. — end note]

## 6 A thread of execution makes progress when an execution step occurs or a lock-free execution does not complete because there are other concurrent threads that are not blocked in a standard library function (see above).

## 7 For a thread of execution providing concurrent forward progress guarantees, the implementation ensures that the thread will eventually make progress for as long as it has not terminated.

[Note 5: This is required regardless of whether or not other threads of executions (if any) have been or are making progress. To eventually fulfill this requirement means that this will happen in an unspecified but finite amount of time. — end note]

## 8 It is implementation-defined whether the implementation-created thread of execution that executes main (6.9.3.1) and the threads of execution created by std::thread (32.4.3) or std::jthread (32.4.4) provide concurrent forward progress guarantees. General-purpose implementations should provide these guarantees.

## 9 For a thread of execution providing parallel forward progress guarantees, the implementation is not required to ensure that the thread will eventually make progress if it has not yet executed any execution step; once this thread has executed a step, it provides concurrent forward progress guarantees.

## 10 [Note 6: This does not specify a requirement for when to start this thread of execution, which will typically be specified by the entity that creates this thread of execution. For example, a thread of execution that provides concurrent forward progress guarantees and executes tasks from a set of tasks in an arbitrary order, one after the other, satisfies the requirements of parallel forward progress for these tasks. — end note]

## 11 For a thread of execution providing weakly parallel forward progress guarantees, the implementation does not ensure that the thread will eventually make progress.

## 12 [Note 7: Threads of execution providing weakly parallel forward progress guarantees cannot be expected to make progress regardless of whether other threads make progress or not; however, blocking with forward progress guarantee delegation, as defined below, can be used to ensure that such threads of execution make progress eventually. — end note]

## 13 Concurrent forward progress guarantees are stronger than parallel forward progress guarantees, which in turn are stronger than weakly parallel forward progress guarantees.

[Note 8: For example, some kinds of synchronization between threads of execution are only guaranteed to make progress if the respective threads of execution provide parallel forward progress guarantees, but will not necessarily make progress under weakly parallel guarantees. — end note]

## 14 When a thread of execution P is specified to block with forward progress guarantee delegation on the completion of a set S of threads of execution, then throughout the whole time of P being blocked on S, the implementation shall ensure that the forward progress guarantees provided by at least one thread of execution in S is at least as strong as P’s forward progress guarantees.

[Note 9: It is unspecified which thread or threads of execution in S are chosen and for which number of execution steps. The strengthening is not permanent and not necessarily in place for the rest of the lifetime of the affected thread of execution. As long as P is blocked, the implementation has to eventually select and potentially strengthen a thread of execution in S. — end note]

Once a thread of execution in S terminates, it is removed from S. Once S is empty, P is unblocked.

## 15 [Note 10: A thread of execution B thus can temporarily provide an effectively stronger forward progress guarantee for a certain amount of time, due to a second thread of execution A being blocked on it with forward progress guarantee delegation. In turn, if B then blocks with forward progress guarantee delegation on C, this can also temporarily provide a stronger forward progress guarantee to C. — end note]

## 16 [Note 11: If all threads of execution in S finish executing (e.g., they terminate and do not use blocking synchronization incorrectly), then P’s execution of the operation that blocks with forward progress guarantee delegation will not result in P’s progress guarantee being effectively weakened. — end note]

## 17 [Note 12: This does not remove any constraints regarding blocking synchronization for threads of execution providing parallel or weakly parallel forward progress guarantees because the implementation is not required to strengthen a particular thread of execution whose too-weak progress guarantee is preventing overall progress. — end note]
