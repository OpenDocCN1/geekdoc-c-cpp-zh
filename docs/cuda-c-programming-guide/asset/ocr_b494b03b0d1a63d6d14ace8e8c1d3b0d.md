# F.3.4. Pointers

Dereferencing a pointer either to global or shared memory in code that is executed on the host, or to host memory in code that is executed on the device results in an undefined behavior, most often in a segmentation fault and application termination.

The address obtained by taking the address of a __device__, __shared__ or __constant__ variable can only be used in device code. The address of a __device__ or __constant__ variable obtained through cudaGetSymbolAddress() as described in Device Memory can only be used in host code.

# F.3.5. Operators

# F.3.5.1. Assignment Operator

__constant__ variables can only be assigned from the host code through runtime functions (Device Memory); they cannot be assigned from the device code.

__shared__ variables cannot have an initialization as part of their declaration.

It is not allowed to assign values to any of the built-in variables defined in Built-in Variables.

# F.3.5.2. Address Operator

It is not allowed to take the address of any of the built-in variables defined in Built-in Variables.

# F.3.6. Run Time Type Information (RTTI)

The following RTTI-related features are supported in host code, but not in device code.

+   - typeid operator
+   - std::type_info
+   - dynamic_cast operator

# F.3.7. Exception Handling

Exception handling is only supported in host code, but not in device code.

Exception specification is not supported for __global__ functions.

# F.3.8. Standard Library

Standard libraries are only supported in host code, but not in device code, unless specified otherwise.

# F.3.9. Functions