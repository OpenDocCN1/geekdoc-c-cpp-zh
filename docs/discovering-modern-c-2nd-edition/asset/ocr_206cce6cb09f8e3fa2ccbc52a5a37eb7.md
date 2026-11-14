Click here to view code image

Click here to view code image

```
std::unique_ptr<double> f()
{
    return std::unique_ptr<double>( new double ); }

int main ()
{
    unique_ptr<double> dp3;
    dp3 = f();
}
```

In this case, move() is not needed since the function result is a temporary that will be moved (again, details in §2.3.5).

Unique pointer has a special implementation<sup>21</sup> for arrays. This is necessary for properly releasing the memory (with delete[]). In addition, the specialization provides array-like access to the elements:

Click here to view code image

```
unique_ptr<double[]> da(new double[3]);
for (unsigned i = 0; i < 3; ++i)
    da[i] = i+2;
```

21. Specialization will be discussed in §3.5.1 and §3.5.3.

In return, the operator* is not available for arrays.

An important benefit of unique_ptr is that it has absolutely no overhead over raw pointers: neither in time nor in memory.

**Further reading:** An advanced feature of unique pointers is to provide its own _Deleter_; for details see [40, §5.2.5f], [62, §34.3.1], or an online reference (e.g., cppreference.com).

# C++11 1.8.3.2 Shared Pointer

As its name indicates, a _shared_ptr_ manages memory that is shared between multiple parties (each holding a pointer to it). The memory is automatically released as soon as no _shared_ptr_ is referring the data any longer. This can simplify a program considerably, especially with complicated data structures. An extremely important application area is concurrency: the memory is automatically freed when all threads have