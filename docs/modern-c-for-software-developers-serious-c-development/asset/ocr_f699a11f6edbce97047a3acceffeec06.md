```
taker(q);
// memory allocated to q is freed when the scope of
// taker is exited.
if (q == nullptr)
{
    std::cout << "q destroyed in taker()";
}
```

```
// output
in calc function 0x7ffe994e530
q was not destroyed in calc
ownership taken: 0x7ffe994e508
q destroyed in taker()
```

# Deleting std::unique_ptr

Normally a std::unique_ptr object will automatically delete the pointer that it wraps when the smart pointer object leaves scope. However we can manually delete a smart pointer object with sp.reset().

# Releasing A unique_ptr To A Raw Pointer

A unique_ptr object can also release itself to the raw pointer that it wraps:

```
double* raw_pointer = new double[50];
std::unique_ptr<double[]> sp(raw_pointer);
raw_ptr = sp.release();
```

After the release, the smart pointer object will be destroyed.