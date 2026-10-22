# Atomics Support: stdatomic.h (C11)

This header file, along with threads.h, provides support for concurrent programming. This topic is well beyond the scope of this book, but, in general terms, the stdatomic.h header file provides macros for creating atomic operations. The programming community uses the term atomic as Democritus did in his theory of matter, meaning indivisible. An operation, such as assigning one structure to another, may appear to be atomic at the programming level but may consist of multiple steps at the machine language level. If a program is split into multiple threads, one thread might read or modify data that a second thread is in the process of using. You could, for instance, wind up with a chimera of a structure having some members assigned values by one thread and other members assigned values by a different thread. The stdatomic.h header file enables you to create operations that act as if they were atomic so that one thread cannot interrupt the work of another thread.

# Boolean Support: stdbool.h (C99)

This header file defines the four macros shown in Table RS.V.23.

# Table RS.V.23 The stdbool.h Macros

| Macro | Description |
|---|---|
| bool | Expands to _Bool |
| false | Expands to the integer constant 0 |
| true | Expands to the integer constant 1 |
| __bool_true_false_are_defined | Expands to the integer constant 1 |

# Common Definitions: stddef.h

This header file defines some types and macros, as shown in Tables RS.V.24 and RS.V.25

# Table RS.V.24 The stddef.h Types

| Type | Description |
|---|---|
| ptrdiff_t | A signed integer type for representing the result of subtracting one pointer from another |
| size_t | An unsigned integer type representing the result of the sizeof operator |
| wchar_t | An integer type that can represent the largest extended character set specified by supported locales |