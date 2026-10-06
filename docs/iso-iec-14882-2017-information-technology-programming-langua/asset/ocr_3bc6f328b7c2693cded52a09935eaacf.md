# ISO/IEC 14882:2017(E)

release operation on those locations. Locally, performing a release operation on A forces prior side effects on other memory locations to become visible to other threads that later perform a consume or an acquire on A. “Relaxed” atomic operations are not synchronization operations even though, synchronization operations, cannot contribute to data races. — end note

+   4 Modifications to a particular atomic object M in some particular total order, combined the modification order of M. [Note: There is a separate order for each atomic object. There is no requirement that these be combined into a single total order for all objects. In general this will be impossible if different threads observe modifications to different objects in different orders. — end note

+   5 A release sequence defined by a release operation A on an atomic object M is a maximum contiguous sequence of side effects in the modification order of M, where the first operation is A, and every subsequent operation

+   (5.1) is performed by the thread that performed A, or
(5.2) is an atomic read-modify-write.

+   6 Certain library calls synchronize with library calls called by another thread. For example, an atomic store-release synchronizes with a load-acquire that takes its value. Except in the specific cases, reading a value does not necessarily ensure visibility as described below. Such a requirement would seem arbitrary without efficient implementation. Note: The specifications of the synchronization operations define when one reads the value written by another. For atomic objects, the definition is clear. All operations on a mutex acquire in a single total order. Each mutex acquisition “reads the value written” by the last release. — end note

+   7 An acquisition A carries a dependency on B if

+   (7.1) the value of A is used as an operation on B, unless

+   (7.1.1) B is an invocation of any operation of std::kill_dependency(32,4), or
(7.1.2) A is the left operand of a binary-logical AND (&&, see 8.14) or logical OR (||, see 8.15) operator, or

+   (7.3) A is the left operand of a conditional (?:, see 8.16) operator, or
(7.4) A is the left operand of the comma-in (,) operator (see 8.19);

+   (7.2) A writes a scalar object or bit-field M, B reads the value written by A from M, and A is sequenced before B, or

+   (7.3) for some evaluation X, A carries a dependency to X, and X carries a dependency to B.
[Note: “carries a dependency” is a subset of “sequenced before”, and is strictly strictly intra-thread. — end note

+   8 An evaluation A is dependency-ordered before an evaluation B if

+   (8.1) A performs an operation on an atomic object M, and in another thread, B performs a consume operation on M and reads the value written by any side effect in the release sequence headed by A, or
(8.2) for some evaluation X, A is dependency-ordered before X and X carries a dependency to B.

[Note: The relation “dependency-ordered before” is analogous to “synchronizes with”, but uses release/- in place of release/acquire. — end note

+   9 An evaluation A inter-thread happens before an evaluation B if

+   (9.1) A synchronizes with B, or
(9.2) A is dependency-ordered before B, or