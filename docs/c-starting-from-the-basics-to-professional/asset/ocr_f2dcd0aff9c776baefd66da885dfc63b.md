# CHAPTER 16: RUNTIME ERRORS AND EXCEPTIONS

with this operation and allow the user to continue. But that does not mean you are out of the woods! Can you spot what else has gone wrong with this program?

The computeValues() function allocates an array of double values in the free store, attempts to fill them, and then returns the array to its caller. It is the responsibility of the caller—in this case main()—to deallocate this memory. However, because an exception is thrown halfway through the execution of computeValues(), its values array is never actually returned to main(). Therefore, the array is never deallocated either. In other words, we have just leaked an array of 10,000 doubles!

Assuming computeValue() inherently leads to the occasional Trouble exception, the only place where we can fix this leak is in the computeValues() function. After all, main() never even receives a pointer to the leaked memory, so there is little that can be done about it there. In the spirit of this chapter thus far, a first obvious solution would therefore be to add a try block to computeValues() as follows (you can find this solution in Ex16_07A):

```
```cpp
double* computeValues(size_t howMany)
{
    double* values{ new double[howMany] };
    try
    {
        for (size_t i {0}; i < howMany; ++i)
            values[i] = computeValue(i);
        return values;
    }
    catch (const Trouble&)
    {
        std::cout << "I sense trouble... Freeing memory..." << std::endl;
        delete[] values;
        throw;
    }
}
```
```

Notice that values has to be defined outside the try block. Otherwise, the variable would be local to the try block, and we could not refer to it anymore from within the catch block. If you redefine computeValues() like this, no further changes are required to the rest of the program. It will also still have a similar outcome, except that this time the values array is not leaked:

```
```
I sense trouble... Freeing memory...
No worries: I've caught it!
```
```

While this computeValues() with the try block makes for a perfectly correct program, it is not the most recommended approach. The function's code has become about twice as long and about twice as complicated as well. The next section introduces better solutions that do not suffer these shortcomings.

# Resource Acquisition Is Initialization

One of the hallmarks of modern C++ is the so-called RAII idiom, short for “resource acquisition is initialization.” Its premise is that each time you acquire a resource you should do so by initializing an object. Memory in the free store is a resource, but other examples include file handles (while holding these, other processes often may not access a file), mutexes (used for synchronization in concurrent programming), network connections, and so on. As per RAII, every such resource should be managed by an object, either