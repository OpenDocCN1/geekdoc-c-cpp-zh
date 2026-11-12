# F.3.9.1. External Linkage

A call within some device code of a function declared with the extern qualifier is only allowed if the function is defined within the same compilation unit as the device code, i.e., a single file or several files linked together with relocatable device code and nvlink.

# F.3.9.2. Implicitly-declared and explicitly-defaulted functions

Let F denote a function that is either implicitly declared or is explicitly defaulted on its first declaration. The execution space specifiers (__host__, __device__) for F are the union of the execution space specifiers of all the functions that invoke it (note that a __global__ caller will be treated as a __device__ caller for this analysis). For example:

```
class Base {
int x;
public:
__host__ __device__ Base(void) : x(10) {}
};
class Derived : public Base {
int y;
};
class Other: public Base {
int z;
};
__device__ void foo(void)
{
Derived D1;
Other D2;
}
__host__ void bar(void)
{
Other D3;
}
```

Here, the implicitly-declared constructor function "Derived::Derived" will be treated as a __device__ function, since it is invoked only from the __device__ function "foo". The implicitly-declared constructor function "Other::Other" will be treated as a __host__ __device__ function, since it is invoked both from a __device__ function "foo" and a __host__ function "bar".

In addition, if F is a virtual destructor, then the execution spaces of each virtual destructor D overridden by F are added to the set of execution spaces for F, if it is either not implicitly defined or is explicitly defaulted on a declaration other than its first declaration.