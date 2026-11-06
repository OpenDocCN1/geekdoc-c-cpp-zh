&lhs, Y const &rhs), and operator+(X const &lhs, X const &rhs) might all exist. So, if the conversion operator exists, then depending on the kind of overload of operator+ that is defined either the addition’s left-hand side operand (#6), right-hand side operand (#7), or operator+ itself (#8) may throw an exception. The resulting value may again be of any type and so the overloaded cout << return-type-of-operator+ operator may throw an exception (#9). Since operator+ returns a temporary object it is destroyed shortly after its use. X’s destructor could throw an exception (#10).

+   - `delete xp`: whenever operator new is overloaded operator delete should be overloaded as well and may throw an exception (#11). And of course, X’s destructor might again throw an exception (#12).
+   - `}`: when the function terminates the local x object is destroyed: again an exception could be thrown (#13).

It is stressed here (and further discussed in section 10.11) that although it is possible for exceptions to leave destructors this would violate the C++ standard and so it must be prevented in well-behaving C++ programs.

How can we expect to create working programs when exceptions might be thrown at this many situations?

Exceptions may be generated in a great many situations, but serious problems are prevented when we’re able to provide at least one of the following exception guarantees:

+   - The *basic guarantee*: no resources are leaked. In practice this means: all allocated memory is properly returned when exceptions are thrown.
+   - The *strong guarantee*: the program’s state remains unaltered when an exception is thrown (as an example: the canonical form of the overloaded assignment operator provides this guarantee)
+   - The *nothrow guarantee*: this applies to code for which it can be proven that no exception can be thrown from it.

# 10.9.1  The basic guarantee

The *basic guarantee* dictates that functions that fail to complete their assigned tasks must return all allocated resources, usually memory, before terminating. Since practically all functions and operators may throw exceptions and since a function may repeatedly allocate resources the blueprint of a function allocating resources shown below defines a try block to catch all exceptions that might be thrown. The catch handler’s task is to return all allocated resources and then rethrow the exception.

```
void allocator(X **xDest, Y **yDest)
{
    X *xp = 0;                 // non-throwing preamble
    Y *yp = 0;

    try                         // this part might throw
    {
        xp = new X[nX];         // alternatively: allocate one object
        yp = new Y[nY];
    }
    catch(...)
    {
        delete xp;
        throw;
    }

    delete[] *xDest;            // non-throwing postamble
```