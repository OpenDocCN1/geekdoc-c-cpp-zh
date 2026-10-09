# Function Pointers Map to Delegates

One last key point related to P/Invoke is that function pointers in unmanaged code map to delegates in managed code. To set up a timer, for example, you would provide a function pointer that the timer could call back on, once it had expired. Specifically, you would pass a delegate instance that matches the signature of the callback.

# Guidelines

Given the idiosyncrasies of P/Invoke, there are several guidelines to aid in the process of writing such code.

![](bbox=[0.14, 0.34, 0.82, 0.73])

# Pointers and Addresses

On occasion, developers may want to access and work with memory, and with pointers to memory locations, directly. This is necessary, for example, for certain operating system interactions as well as with certain types of time-critical algorithms. To support this capability, C# requires use of the unsafe code construct.