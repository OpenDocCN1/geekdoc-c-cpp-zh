When both a const and a non-const version of a function are present, the compiler automatically chooses the correct version, depending on whether the function was activated by a constant node (such as `const node *c`) or by an ordinary node.

**When to Provide Both Const and Non-Const Versions of a Member Function**

When the return value of a member function is a pointer to a node, you should generally have two versions: a const version that returns a `const node*`; and an ordinary version that returns an ordinary pointer to a node.

# DEREFERENCING THE NULL POINTER

One of the most common pointer errors is writing the expression *p or p-> when the value of the pointer p is the null pointer. This must always be avoided because the null pointer does not point to anything. Therefore, when p is the null pointer, *p (which means "the thing that p points to") is meaningless. In this case, p-> is also meaningless. Because the asterisk in *p is called the dereferencing operator, we can state this rule: Never dereference the null pointer.

Accidental dereferencing of the null pointer is sometimes a hard error to track down. The error does not cause a syntax error. Instead, when the program is running, there will be an attempt to interpret the null pointer as if it were a valid address. Sometimes this causes an immediate run-time error with a message such as "Address protection violation" or "Bus error, core dumped." But on other machines, the null address might be a valid address, causing your program to read or write an unintended memory location. Often this memory location is part of the machine's operating system, resulting in part of the operating system being corrupted. At some later point, perhaps after your program has completed, the corrupted operating system can cause an error. Fortunately, restarting your machine usually writes a fresh copy of the operating system into memory—but even so, never dereference the null pointer!

# Self-Test Exercises for Section 5.1

+   1. Write the class definition needed for a node in a linked list. Use the name value_type for the type of the data.
+   2. What is the meaning of the C++ constant NULL? What additional code is needed in a program in order to use NULL?
+   3. Describe two common uses for the null pointer.