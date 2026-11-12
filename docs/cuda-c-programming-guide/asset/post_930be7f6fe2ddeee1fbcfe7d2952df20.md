
- formal parameters,
- non-extern variable declarations within a function that executes on the host.

The `__device__`, `__constant__` and `__managed__` memory space specifiers are not allowed on variable declarations that are neither extern nor static within a function that executes on the device.

A `__device__`, `__constant__`, `__managed__` or `__shared__` variable definition cannot have a class type with a non-empty constructor or a non-empty destructor. A constructor for a class type is considered empty at a point in the translation unit, if it is either a trivial constructor or it satisfies all of the following conditions:

- The constructor function has been defined.
- The constructor function has no parameters, the initializer list is empty and the function body is an empty compound statement.
- Its class has no virtual functions and no virtual base classes.
- The default constructors of all base classes of its class can be considered empty.
- For all the nonstatic data members of its class that are of class type (or array thereof), the default constructors can be considered empty.

A destructor for a class is considered empty at a point in the translation unit, if it is either a trivial destructor or it satisfies all of the following conditions:

- The destructor function has been defined.
- The destructor function body is an empty compound statement.
- Its class has no virtual functions and no virtual base classes.
- The destructors of all base classes of its class can be considered empty.
- For all the nonstatic data members of its class that are of class type (or array thereof), the destructor can be considered empty.

When compiling in the whole program compilation mode (see the nvcc user manual for a description of this mode), `__device__`, `__shared__`, `__managed__` and `__constant__` variables cannot be defined as external using the `extern` keyword. The only exception is for dynamically allocated `__shared__` variables as described in `__shared__`.

When compiling in the separate compilation mode (see the nvcc user manual for a description of this mode), `__device__`, `__shared__`, `__managed__` and `__constant__` variables can be defined as external using the `extern` keyword. `nvlink` will generate an error when it cannot find a definition for an external variable (unless it is a dynamically allocated `__shared__` variable).

## F.3.3.2. `__managed__` Memory Space Specifier

Variables marked with the `__managed__` memory space specifier ("managed" variables) have the following restrictions:

- The address of a managed variable is not a constant expression.
- A managed variable shall not have a const qualified type.
- A managed variable shall not have a reference type.
- The address or value of a managed variable shall not be used when the CUDA runtime may not be in a valid state, including the following cases:
  - In static/dynamic initialization or destruction of an object with static or thread local storage duration.
  - In code that executes after exit() has been called (e.g., a function marked with gcc's "__attribute__((destructor))").
  - In code that executes when CUDA runtime may not be initialized (e.g., a function marked with gcc's "__attribute__((constructor))").
- A managed variable cannot be used as an unparenthesized id-expression argument to a decltype() expression.
- Managed variables have the same coherence and consistency behavior as specified for dynamically allocated managed memory.
- When a CUDA program containing managed variables is run on an execution platform with multiple GPUs, the variables are allocated only once, and not per GPU.
- A managed variable declaration without the extern linkage is not allowed within a function that executes on the host.
- A managed variable declaration without the extern or static linkage is not allowed within a function that executes on the device.

Here are examples of legal and illegal uses of managed variables:

```
__device__ __managed__ int xxx = 10; // OK
int *ptr = &xxx; // error: use of managed variable
// (xxx) in static initialization
struct S1_t {
int field;
S1_t(void) : field(xxx) {};
};
struct S2_t {
S2_t(void) { xxx = 10; }
};
S1_t temp1; // error: use of managed variable
// (xxx) in dynamic initialization
S2_t temp2; // error: use of managed variable
// (xxx) in the destructor of
// object with static storage
// duration
__device__ __managed__ const int yyy = 10; // error: const qualified type
__device__ __managed__ int &zzz = xxx; // error: reference type
template <int *addr> struct S3_t {};
S3_t<&xxx> temp; // error: address of managed
// variable (xxx) not a
// constant expression
__global__ void kern(int *ptr)
{
assert(ptr == &xxx); // OK
xxx = 20; // OK
}
int main(void)
{
int *ptr = &xxx; // OK
kern<<<1,1>>>(ptr);
cudaDeviceSynchronize();
decltype(xxx) qqq; // error: managed variable (xxx) used
// as unparenthesized argument to
// decltype
decltype((xxx)) zzz = yyy; // OK
}
```

## F.3.3.3. Volatile Qualifier

The compiler is free to optimize reads and writes to global or shared memory (for example, by caching global reads into registers or L1 cache) as long as it respects the memory ordering semantics of memory fence functions (Memory Fence Functions) and memory visibility semantics of synchronization functions (Synchronization Functions).

These optimizations can be disabled using the **volatile** keyword: If a variable located in global or shared memory is declared as volatile, the compiler assumes that its value can be changed or used at any time by another thread and therefore any reference to this variable compiles to an actual memory read or write instruction.

## F.3.4. Pointers

Dereferencing a pointer either to global or shared memory in code that is executed on the host, or to host memory in code that is executed on the device results in an undefined behavior, most often in a segmentation fault and application termination.

The address obtained by taking the address of a __device__, __shared__ or __constant__ variable can only be used in device code. The address of a __device__ or __constant__ variable obtained through cudaGetSymbolAddress() as described in Device Memory can only be used in host code.

## F.3.5. Operators

### F.3.5.1. Assignment Operator

__constant__ variables can only be assigned from the host code through runtime functions (Device Memory); they cannot be assigned from the device code.

__shared__ variables cannot have an initialization as part of their declaration.

It is not allowed to assign values to any of the built-in variables defined in Built-in Variables.

### F.3.5.2. Address Operator

It is not allowed to take the address of any of the built-in variables defined in Built-in Variables.

## F.3.6. Run Time Type Information (RTTI)

The following RTTI-related features are supported in host code, but not in device code.

- typeid operator
- std::type_info
- dynamic_cast operator

## F.3.7. Exception Handling

Exception handling is only supported in host code, but not in device code.

Exception specification is not supported for __global__ functions.

## F.3.8. Standard Library

Standard libraries are only supported in host code, but not in device code, unless specified otherwise.

## F.3.9. Functions

### F.3.9.1. External Linkage

A call within some device code of a function declared with the extern qualifier is only allowed if the function is defined within the same compilation unit as the device code, i.e., a single file or several files linked together with relocatable device code and nvlink.

### F.3.9.2. Implicitly-declared and explicitly-defaulted functions

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
