implementation of
software infrastructure (e.g., device drivers, communications stacks, virtual machines,
operating
systems, operations systems, programming environments, and foundation libraries) is
mostly systems programming. The importance of the “bias toward systems programming”
qualification in
my long-standing characterization of C++ is that C++ has not been simplified
(compromised) by
ejecting the facilities aimed at the expert-level use of hardware and systems resources in
the hope
of making it more suitable for other application areas.
Of course, you can also program in ways that completely hide hardware, use expensive
abstractions (e.g., every object on the free store and every operation a virtual function),
use inelegant styles
(e.g., overabstraction), or use essentially no abstractions (“glorified assembly code”).
However,
many languages can do that, so those are not distinguishing characteristics of C++. The
*Design and Evolution of C++* book [Stroustrup,1994] (known as *D&E*) outlines the ideas
and design aims of C++ in greater detail, but two principles should be noted:

+   - *Leave no room for a lower-level language below C++* (except for assembly code in rare cases). If you can write more efficient code in a lower-level language then that language will most likely become the systems programming language of choice.
+   - *What you don’t use you don’t pay for.* If programmers can hand-write reasonable code to simulate a language feature or a fundamental abstraction and provide even slightly better performance, someone will do so, and many will imitate. Therefore, a language feature and a fundamental abstraction must be designed not to waste a single byte or a single processor cycle compared to equivalent alternatives. This is known as *the zero-overhead principle.*

These are Draconian principles, but essential in some (but obviously not all) contexts. In particular,
the zero-overhead principle repeatedly led C++ to simpler, more elegant, and more powerful facilities than were first envisioned. The STL is an example (§4.1.1, §4.4, §4.5, Chapter 31, Chapter 32, Chapter 33). These principles have been essential in the effort to raise the level of programming.

# 1.2.1 Programming Style

Languages features exist to provide support for programming styles. Please don’t look at an individual language feature as a solution, but as one building brick from a varied set which can be combined to express solutions.

The general ideals for design and programming can be expressed simply:

+   - Express ideas directly in code.
+   - Express independent ideas independently in code.
+   - Represent relationships among ideas directly in code.
+   - Combine ideas expressed in code freely – where and only where combinations make