Many of the CLR's thread synchronization constructs are really just object-oriented class wrappers around Win32 thread synchronization constructs. After all, CLR threads are Windows threads, which means that Windows schedules and controls the synchronization of threads. Windows thread synchronization constructs have been around since 1992, and a ton of material has been written about them.⁴ Therefore, I give them only cursory treatment in this chapter.

# # User-Mode Constructs

There are two kinds of primitive user-mode thread synchronization constructs:

+   - Volatile constructs, which perform an atomic read *or* write operation on a variable containing a simple data type
+   - Interlocked constructs, which perform an atomic read *and* write operation on a variable containing a simple data type

All the volatile and interlocked constructs require you to pass a reference (memory address) to a variable containing a simple data type. Some CPU architectures require that this memory address be properly aligned or else the constructs will throw a `DataMisalignedException`.

This means that a variable containing a 1-byte, 2-byte, and 4-byte value must be located at a memory address that is a multiple of 1, 2, or 4, respectively, and that a variable containing an 8-byte value is located at a memory address that allows the value to be manipulated atomically by the underlying hardware (a multiple of 4 or 8). Specifically, this means **(S)Byte** variables are on a 1-byte boundary, **(U)Int16** variables are on a 2-byte boundary, **(U)Int32** and **Single** variables are on a 4-byte boundary, and **(U)Int64** and **Double** variables are on a 4-byte or an 8-byte boundary. All reference variables and **(U)IntPtr** variables are 4 bytes wide in a 32-bit process and 8 bytes wide in a 64-bit process, so these variables are always aligned on 4-byte or 8-byte boundaries, depending on the type of process.

Fortunately, the CLR ensures that fields are properly aligned automatically unless the enclosing type has the `[StructLayout(LayoutKind.Explicit)]` attribute applied to it and `[FieldOffset(..)]` attributes applied to individual fields, forcing fields to be misaligned. If you avoid using these attributes, then you should have no trouble when using these user-mode constructs.

Accessing any properly aligned variable of the types mentioned above is always atomic. This means that all bytes within that variable are read from or written to all at once. So, for example, if you have the following class: