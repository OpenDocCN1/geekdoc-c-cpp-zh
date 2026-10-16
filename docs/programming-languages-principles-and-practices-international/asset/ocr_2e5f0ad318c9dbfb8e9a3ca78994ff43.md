as **storage semantics** or **value semantics**. Java, for example, uses assignment by sharing for all object variables, but not for simple data; see Section 7.7 for an example. Other languages that use reference semantics are Smalltalk, LISP, and Python.

Figure 7.40 shows assignment by sharing, with the name x being associated directly to a new location (that of y). This is difficult to achieve for a compiler, since the symbol table commonly does not exist during execution. Standard implementations of assignment by sharing (such as in Java) use pointers and implicit dereferencing. In this view of assignment by sharing, x and y are implicitly pointers (with implicit automatically allocated pointer values).

![](bbox=[0.28, 0.265, 0.72, 0.405])

Figure 7.40 Variables as implicit references to objects

Then the assignment x = y has the effect shown in Figure 7.41. Note that this is the same as if we wrote x = y for pointer variables x and y in C.

![](bbox=[0.275, 0.475, 0.72, 0.61])

Figure 7.41 Assignment by sharing of references

However, in the absence of address-of and dereference operators (& and * in C), this implementation is indistinguishable from the original picture. (See Exercise 7.25 and Section 7.7.1.)

# 7.6.2 Constants

A **constant** is a language entity that has a fixed value for the duration of its existence in a program. As shown in Figure 7.42, a constant is like a variable, except that it has no location attribute, but a value only.

![](bbox=[0.275, 0.77, 0.72, 0.825])

Figure 7.42 A constant and its attributes