# ISO/IEC 14882:2017(E)

lock_free(A) yields true.

+   3 An evaluation is signal-safe unless it includes one of the following:
(3.1) — call to any standard library function, except for plain lock-free atomic operations and functions that rely on a library-provided memory allocator. [Note: This excludes the use of new and delete expressions — end note]
(3.2) — access to an object with thread storage duration;
(3.3) — a dynamic_cast expression;
(3.4) — throwing of an exception;
(3.5) — control entering a try-block or function-try-block;
(3.6) — initialization of a variable with static storage duration requiring dynamic initialization (6.6.3, 9.7)$220; or
(3.7) — waiting for the completion of the initialization of a variable with static storage duration (9.7).
A signal handler invocation has undefined behavior if it includes an evaluation that is not signal-safe.

+   4 The function signal is signal-safe if it is invoked with the first argument equal to the signal number corresponding to the signal that caused the invocation of the handler.

SEE ALSO: ISO C 7.14

> 220 Such initialization might not occur because it is the first odr-use (6.2) of that variable.

§ 21.10.4 ©ISO/IEC 2017 – All rights reserved 510