```
int main()
{
    memory_address();
}

// output
address of created sp = 0x7fff565e8488
in borrower1. memory address of pointer to = 0x7fff565e8488
in borrower2. memory address of reference to sp = 0x7fff565e8488
```

# Moving A unique_ptr

If an owner wants to yield it's ownership of a std::unique_ptr object to another variable, it must use std::move.

```
#include <iostream>
#include <memory>
#include <utility> // required header for std::move

void calc(std::unique_ptr<double>&& x)
{
    std::cout << "in calc function " << x << std::endl;
}

void taker(std::unique_ptr<double>&& x)
{
    std::unique_ptr<double> d = std::move(x);
    std::cout << "ownership taken: " << d << std::endl;
}

int main()
{
    // p is created and owns a contiguous block of memory
    // containing 42 double numbers
    std::unique_ptr<double[]> p(new double[42]);

    // move p to q
    std::unique_ptr<double[]> q = std::move(p);

    calc(q);

    if (q != nullptr)
    {
        std::cout << "q was not destroyed in calc" << std::endl;
    }

    // move q into the argument of the taker function
```