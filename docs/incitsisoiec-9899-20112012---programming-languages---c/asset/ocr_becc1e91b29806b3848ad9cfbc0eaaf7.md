A visible side effect on an object M with respect to a value computation B of M satisfies the condition:

+   - A happens before B, and
- there is no other side effect X to M such that A happens before X and X happens before B.

The value of a non-atomic scalar object M, as determined by evaluation B, shall be the value stored by the visible side effect A.

NOTE 8 If there is ambiguity about which side effect to a non-atomic object is visible, then there is a data race and the behavior is undefined.

NOTE 9 This states that operations on ordinary variables are not visibly reordered. This is not actually detectable without data races, but it is necessary to ensure that data races, as defined here, and with suitable restrictions on the use of atomics, correspond to data races in a simple interleaved (sequentially consistent) execution.

The visible sequence of side effects on an atomic object M, with respect to a value computation of B, is a maximal sub-sequence of side effects in the modification order of M, where the first side effect is visible with respect to B, and for every subsequent side effect, it is not the case that B happens before it. The value of an atomic object M, as determined by B, shall be the value stored by some operation in the visible sequence of M with respect to B. Furthermore, if a value computation A of an atomic M happens before a stored side effect X, then the value computed by B shall either equal the value computed by A, or the value stored by side effect Y, where Y follows X in the modification order of M.

NOTE 10 This effectively disables compiler reordering of atomic operations to a single object, even if both operations are "relaxed" loads. By doing so, we effectively make the "cache coherence" guarantee provided by hardware atomic operations.

NOTE 11 The visible sequence depends on the "happens before" relation, which in turn depends on the values observed by loads of atomics, which we are restricting here. The intended relation is that there must exist an association of atomic loads with modifications they observe, together with suitably chosen modification orders and the "happens before" relation derived as described above, satisfying the imposed here.

The execution of a program contains a data race if it contains two conflicting actions in different threads, at least one of which is not atomic, and neither happens before the other. Any other data race results in undefined behavior.

NOTE 12 It can be shown that programs correctly use simple mutexes and memory_order_seq_cast operations to prevent all data races, and use no other synchronization operations, behave as the operations executed by their constituent threads were simply interleaved, with each value computation of an atomic being the last value stored in interleaving. This is normally referred to as "sequential consistency". However, this applies only to data-free programs, and data-free programs cannot observe most transformations that do not change single-threaded semantics. In fact, most single-threaded program transformations continue to be allowed, since any program that behaves differently as a result must contain undefined behavior.