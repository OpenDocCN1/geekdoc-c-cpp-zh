The definition of C++ is the ISO C++ standard, but that document is neither intended for nor suitable for novices. Don’t forget to use your online documentation. If you look at this appendix while working on the early chapters, expect much to be “mysterious,” as explained in later chapters.

For standard library facilities, see Appendix B.

The standard for C++ is defined by a committee working under the auspices of the ISO (the international organization for standards) in collaboration with national standards bodies, such as INCITS (United States), BSI (United Kingdom), and AFNOR (France). The current definition is ISO/IEC 14882:2011 *Standard for Programming Language C++*.

# ### A.1.1 Terminology

The C++ standard defines what a C++ program is and what the various constructs mean:

+   * *Conforming*: A program that is C++ according to the standard is called *conforming* (or colloquially, *legal* or *valid*).
* *Implementation defined*: A program can (and usually does) depend on features (such as the size of an `int` and the numeric value of `'a'`) that are only well defined on a given compiler, operating system, machine architecture, etc. The implementation-defined features are listed in the standard and must be documented in implementation documentation, and many are reflected in standard headers, such as `<limits>` (see §B.1.1). So, being conforming is not the same as being portable to all C++ implementations.
* *Unspecified*: The meaning of some constructs is *unspecified*, *undefined*, or *not conforming but not requiring a diagnostic*. Obviously, such features are best avoided. This book avoids them. The unspecified features to avoid include
	* Inconsistent definitions in separate source files (use header files consistently; see §8.3)
	* Reading *and* writing the same variable repeatedly in an expression (the main example is `a[i] = ++i;`)
	* Many uses of explicit type conversion (casts), especially of `reinterpret_cast`

# ### A.1.2 Program start and termination

A C++ program must have a single global function called `main()`. The program starts by executing `main()`. The return type of `main()` is `int` (**void** is *not* a conforming alternative). The value returned by `main()` is the program’s return value to “the system.” Some systems ignore that value, but successful termination is indicated by returning zero and failure by returning a nonzero value or by an uncaught exception (but an uncaught exception is considered poor style).