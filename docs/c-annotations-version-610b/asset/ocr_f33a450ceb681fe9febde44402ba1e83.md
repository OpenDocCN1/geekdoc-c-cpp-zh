```
```cpp
public:
    Incomplete2(size_t nChars, size_t nInts)
    try
    :
        d_composed(/* arguments */),    // might throw
        d_cp(0),
        d_ip(0)
    {
        preamble();                      // might throw
        d_cp = new char[nChars];         // might throw
        d_ip = new int[nChars];          // might throw
        postamble();                      // might throw
    }
    catch (...)
    {
        delete[] d_cp;                   // clean up
        delete[] d_ip;
    }
};
```
```

On the other hand, since C++11 offers constructor delegation an object may have been completely constructed according to the C++ run-time system, but yet its constructor may have thrown an exception. This happens if a delegated constructor successfully completes (after which the object is considered “completely constructed”), but the constructor itself throws an exception, as illustrated by the next example:

```
```cpp
class Delegate
{
    public:
        Delegate()
        :
        {
            Delegate()
            {
                throw 12;        // throws but completely constructed
            }
        Delegate(int x)          // completes OK
        {}
};
int main()
try
{
    Delegate del;                // throws

} // del’s destructor is called here
catch (...)
{}
```
```

In this example it is the responsibility of Delegate’s designer to ensure that the throwing default constructor does not invalidate the actions performed by Delegate’s destructor. E.g., if the delegated constructor allocates memory to be deleted by the destructor, then the default constructor should either leave the memory as-is, or it can delete the memory and set the corresponding pointer to zero thereafter. In any case, it is Delegate’s responsibility to ensure that the object remains in a valid state, even though it throws an exception.

According to the C++ standard exceptions thrown by destructors may not leave their bodies. Providing a destructor with a function try block is therefore a violation of the standard: exceptions caught by a function try block’s catch clause have already left the destructor’s body. If—in violation of the standard—the destructor is provided with a function try block and an exception is caught by the try block then that exception is rethrown, similar to what happens in catch clauses of constructor functions’ try