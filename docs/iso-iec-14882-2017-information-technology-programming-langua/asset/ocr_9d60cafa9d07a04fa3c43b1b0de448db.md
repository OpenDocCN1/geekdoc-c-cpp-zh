# ISO/IEC 14882:2017(E)

3 If a deallocation function terminates with an exception, the value of the first argument supplied to a deallocation function is a null pointer value; if so, and the deallocation function is specified in the standard library, it has no effect.

4 If the argument given to a deallocation function in the standard library is a pointer that is not the null pointer (7.11), the deallocation function shall deallocate the storage referenced by the pointer, ending the duration of the region of storage.

# 6.7.4.3 Safe-derived pointers

1 A traceable pointer object

+   (1.1) an object of pointer type (6.9.2),
(1.2) an object of an integer type that is at least as large as std::intptr_t, or
(1.3) a sequence of elements in an array of narrow type (6.9.1), where the size and alignment of the sequence matches those of some pointer object.

+   2 A pointer is a safe-derived pointer only if it has an object pointer type and it is one of the following:
(2.1) the value returned by a C++ standard library implementation of ::operator new(std::size_t) or ::operator new(std::size_t, std::align_val_t);
(2.2) the result of the address of an object (or one of its subobjects) designated by an lvalue resulting from a traceable object;
(2.3) the result of well-defined pointer arithmetic (8.7) using a safe-derived pointer value;
(2.4) the result of a well-defined conversion (7.11, 8.4) of a safe-derived pointer value;
(2.5) the result of a reinterpret_cast of a safe-derived pointer value;
(2.6) the result of a reinterpret_cast of an integer representation of a safe-derived pointer;
(2.7) the value of an object whose was copied from a traceable pointer object, at the time of the source object contained a copy of a safe-derived pointer value.

3 An value is an integer representation of a safe-derived pointer only if its type is at least large as std::intptr_t and it is one of the following:

+   (3.1) the result of a valid conversion of an integer representation of a safe-derived pointer value;
(3.2) the result of a valid conversion from a traceable pointer object, at the time of the source object contained an integer representation of a safe-derived pointer value;
(3.3) the value of an object whose value was copied from a traceable pointer object, at the time of the source object contained an integer representation of a safe-derived pointer value;
(3.4) the result of an additive or bitwise operation, one of whose is an integer representation of a safe-derived pointer P, if that result converted by reinterpret_cast<void>() would compare P.

4 An implementation may have relaxed pointer, in which case the value of a pointer value does not depend on whether it is a safe-derived pointer. Alternatively, an implementation may have a safe-derived pointer value referring to dynamic storage which is not a safe-derived pointer value unless the referenced complete object has previously been deallocated (5.11.1). Note that any pointer value (including null value passed to a deallocation function) is undefined; 6.7. This is even true if the unsafe-derived pointer value might

(40) This section does not impose restrictions on indirect pointers to memory not allocated by ::operator new. This maintains the ability of many C++ implementations to use binary libraries and components written in other languages. In particular, this applies to C binaries, indirect pointer to memory allocated by std::malloc is not prohibited.