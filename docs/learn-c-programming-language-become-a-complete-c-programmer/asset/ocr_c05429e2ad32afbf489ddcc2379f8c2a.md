```
// no value
}
else {
// use r
}
}
```

Obviously, you need to have suitably defined **nullX**. The style is not idiomatic and I don’t recommend it. A programmer is allowed to assume that a reference is valid. It is possible to create an invalid reference, but you have to go out of your way to do so. For example:

```
char* ident(char * p) { return p; }
char& r {*ident(nullptr)}; // invalid code
```

This code is not valid C++ code. Don’t write such code even if your current implementation doesn’t catch it.

# Section 7.8 Advice 199

# 7.8 Advice

+   [1] Keep use of pointers simple and straightforward; §7.4.1.
+   [2] Avoid nontrivial pointer arithmetic; §7.4.
+   [3] Take care not to write beyond the bounds of an array; §7.4.1.
+   [4] Avoid multidimensional arrays; define suitable containers instead; §7.4.2.
+   [5] Use **nullptr** rather than **0** or **NULL**; §7.2.2.
+   [6] Use containers (e.g., **vector**, **array**, and **valarray**) rather than built-in (C-style) arrays; §7.4.1.
+   [7] Use **string** rather than zero-terminated arrays of **char**; §7.4.
+   [8] Use raw strings for string literals with complicated uses of backslash; §7.3.2.1.
+   [9] Prefer **const** reference arguments to plain reference arguments; §7.7.3.
+   [10] Use rvalue references (only) for forwarding and move semantics; §7.7.2.
+   [11] Keep pointers that represent ownership inside handle classes; §7.6.
+   [12] Avoid **void*** except in low-level code; §7.2.1.
+   [13] Use **const** pointers and **const** references to express immutability in interfaces; §7.5.
+   [14] Prefer references to pointers as arguments, except where “no object” is a reasonable option; §7.7.4.

# *This page intentionally left blank*

+   - Introduction
+   - Structures **struct** Layout; **struct** Names; Structures and Classes; Structures and Arrays; Type Equivalence; Plain Old Data; Fields
+   - Unions
+   Unions and Classes; Anonymous **union**s
+   - Enumerations
+   **enum classes**; Plain **enums**; Unnamed **enums**
+   - Advice