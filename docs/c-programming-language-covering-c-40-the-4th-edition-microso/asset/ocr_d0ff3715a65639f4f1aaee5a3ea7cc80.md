variable-reference:
    expression

In C and C++, a variable-reference is known as an lvalue.

# 5.5 Atomicity of Variable References

Reads and writes of the following data types are atomic: bool, char, byte, sbyte, short, ushort, uint, int, float, and reference types. In addition, reads and writes of enum types with an underlying type in the previous list are also atomic. Reads and writes of other types, including long, ulong, double, and decimal, as well as user-defined types, are not guaranteed to be atomic. Aside from the library functions designed for that purpose, there is no guarantee of atomic read-modify-write, such as in the case of increment.

> > **ERIC LIPPERT** The specification authors make certain assumptions about their readers—for instance, that the reader who cares about atomicity already knows what it is. If you’re not one of those readers, the issue here is that if one thread is writing the long 0x0123456776543210 into a variable currently holding zero, then there might be a moment in time when another thread could read 0x0123456700000000 from that variable. This assignment is not “atomic” because it could happen in two distinct phases: first the top 32 bits, then the bottom 32 bits (or vice versa). The C# language guarantees you that this never happens with 32-bit data types, but makes no guarantees about anything larger.

> > **JON SKEET** There is often confusion between atomicity and other complicated aspects of memory models. In particular, just because an assignment is atomic doesn’t mean it will be necessarily be seen immediately (or, indeed, at all) by other threads, unless synchronization techniques such as volatile variables, locks, or explicit memory barriers are involved.