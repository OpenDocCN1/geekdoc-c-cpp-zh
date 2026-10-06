# ISO/IEC 14882:2017(E)

```
using uintmax_t = unsigned integer type;
using uintptr_t = unsigned integer type; // optional
}
```

+   1 The header defines numerous macros of the form:
[INT_FAST_LEAST(8 32 64)_MIN
[U]INT_FAST_LEAST(8 32 64)_MAX
INTMAX_PTR_MIN
[U]INTMAX_PTR_MAX
(PTRDIFF_SIZE_ATOMIC_WCHAR){MAX_MIN}
SIZE_MAX

plus functions of the form:
[U]INT(8 32 64)_MAX_C

+   2 The header defines all types and macros as the same as the C standard library header <stdlib.h>.
SEE ALSO: ISO C 7:20

# 21.5 Start and termination

> [Note: The header <stdlib.h> (21.2.2) declares the functions described in this subclass. — end note]

```
[[return]] void exit(int status) noexcept;
```

+   2 Effects: This function has the semantics in the C standard library.

+   3 Remarks: The program is terminated without destructors for objects of automatic, thread, or static storage duration and without calling passes to exit(it) (6.6.4). The function _Exit is signal-safe(21.10.4).

```
[[return]] void abort() noexcept;
```

+   4 Effects: This function has the semantics in the C standard library.

+   5 Remarks: The program is terminated without destructors for objects of automatic, thread, or static storage duration and without calling handles passed to exit(it) (6.6.4). The abort is signal-safe(21.10.4).

```
int atexit(void (*handler)(void)) noexcept;
int atexit_s(void (*handler)(void)) noexcept;
```

+   6 Effects: This function registers the function pointed to by f to be called without arguments at normal program duration. It is unspecified whether a call to axit() that does not happen before (4.7) a call to exit(it) will succeed. [Note: The aexit() functions do not introduce a data race (20.5.5). — end note]

+   7 Implementation limits: The implementation should handle the registration of at least 32 functions.

+   8 Returns: The exit() function returns zero if the registration succeeds, nonzero if it fails.

```
[[return]] void exit(int status);
```

+   9 Effects:
— First, objects with thread duration and association with the current thread are destroyed.
Next, objects with static storage duration are destroyed and functions registered by calling exit are called.¹215 See 6.6.4 for the order of destruction and calls. (Automatic objects are not destroyed as a result of calling exit(it).²216

215 A function is called every time it is registered. All are destroyed in a program whose main function (6.6.1) contains no automatic

216 Objects with automatic storage duration are destroyed