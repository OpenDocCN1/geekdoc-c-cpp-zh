# Analysis of C Programs
Although the problem of adding big integers is conceptually similar to that of adding small integers, the two C programs are very different. In the 2nd example, we become so involved in the details of programming with BigInts that we lose sight of the essence of the problem we're trying to solve, making the program difficult to write and understand.

Procedural Details Details the procedural programming model force us to deal with in the 2nd program?

+   - Initialize BigInts in separate statements, such as c = itob(0).
Failing to do this in main() is a frequent source of error.
- Handle temporary variables, such as the variable t in main().
- Convert small integers to BigInts, as in t = itob(300); in main().
- Use functions with distinctive names, like badd() and bmult(), instead of the traditional arithmetic operators.
- Manage storage, as in the calls to bfree() in main().

C++ is not MagicnCode to perform operations on big integers and to handle the details of:

+   - initialization
- temporary variables
- type conversions
- storage management
- etc.

must still be written.

The important difference is that in C++, we can package this code as an ADT such that the programmer who codes the ADT, the provider, handles the complexities, while those who use the ADT, the clients, find it as convenient to use as a built-in data type.