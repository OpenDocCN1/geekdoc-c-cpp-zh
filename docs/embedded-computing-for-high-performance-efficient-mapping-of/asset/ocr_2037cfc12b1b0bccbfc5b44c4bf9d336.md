Regarding the kernel description, OpenCL provides a few extensions to the standard C99 language, namely:

+   Vector data types and operations. Vector data types are defined by the type name (char, uchar, ushort, int, uint, float, long, and ulong) followed by a literal value n which corresponds to the number of elements in the vector. These data types work with standard C operators, such as +, -, and *. The use of vectors in an OpenCL kernel is automatically compiled to exploit SIMD units if the hardware supports it, or to regular scalar code if not.

+   Rounding and conversion routines. As in C99, implicit conversions are supported for compatible scalar data types, whereas explicit conversions are required for incompatible scalar types through casting. OpenCL extends this support for both scalars and vectors with a set of explicit conversion routines with the form: convert_<destination_type>(source), as shown in the following example:

```
int8 i;
// converts an int8 vector to float8
float8 j = convert_float8(i)
```

In addition, OpenCL supports a set of rounding routines with the syntax convert_<destination_type><sat>|_<rounding_mode>(source), where the optional sat mode specifies saturation for out-of-range values to the maximum possible value the destination type can support. There is support for four rounding modes, namely: rte (round to the nearest even), rtp (round toward positive infinity), rtz (round toward zero), and rtn (round toward infinity). If no modifier is specified, it defaults to rtz for integer values and rte for floating point values.

+   Intrinsic functions. OpenCL supports a number of math library functions with guaranteed accuracy, e.g., exp, log, sin, fmax, and modf. OpenCL also supports two additional sets of fast intrinsics versions, which provide a trade-off between precision and performance, in the form of native_<fn> (fastest but no accuracy guarantee) and half_<fn> (less performant than the corresponding native intrinsic but with higher accuracy), e.g., native_log and half_log. The use of intrinsics guarantees availability (all OpenCL compliant devices are meant to support them), thus increasing the portability of OpenCL code across heterogeneous devices.

In addition, OpenCL includes utility functions that provide information about each work-item, allowing the kernel to identify which operation to perform on and which data:

+   Global dimensions: (1) get_global_id(dim): returns a unique global work-item ID for a particular dimension; (2) get_work_dim(): returns the number of global dimensions; (3) get_global_size(dim): returns the maximum number of global work-items in a particular dimension.

+   Local dimensions: (1) get_local_id(dim): returns a unique work-item ID for a particular dimension within its work-group; (2) get_local_size(dim): returns the number of local work-items in particular dimension; (3) get_num_groups