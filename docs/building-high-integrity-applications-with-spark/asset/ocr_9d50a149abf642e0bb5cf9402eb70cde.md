happens that with the GNAT and gcc compilers the two types are compatible, but for maximum portability it is better to use the types in Interfaces.C.

The previous package specification, written with SPARK_Mode on, starts by introducing types for the node identifiers and sequence numbers. The names do not have to be the same as in the C header file; they only need to be used appropriately in the following declarations. In the original C, nodeid_t and sequenceno_t are aliases for C built-in types and can be mixed freely with other unrelated variables having those same types. However, the definitions in package Messages are for entirely new types that cannot be accidentally mixed. This is more robust and is an example of Ada's ability to increase the type safety of a preexisting C interface.

The enumeration is defined as an Ada enumeration with the Convention aspect set to C. This informs the Ada compiler that objects of that type should be represented compatibly with the associated C compiler's handling of enumerations. The ability to set the Convention aspect on an enumeration type is the only GNAT extension we use in this example. Because the C header file defines the enumeration starting at one instead of the default of zero, package Messages uses an *enumeration representation clause* to specify the values of the enumerators in a matching way.⁵

Finally, the C structure is modeled as an Ada record, again using the Convention aspect of C to ensure that the Ada compiler lays out the record in a manner that matches the associated C compiler's expectations for structures.

Armed with these type definitions we can now write declarations for the two C functions in our example. We will start with the checksum computing function because, being a pure function, it is easy to represent in SPARK:

```
```ada
function Compute_Fletcher_Checksum
  (Buffer : in  Interfaces.C.char_array ;
   Size   : in  Interfaces.C.size_t) return Interfaces.C.unsigned_short
with
   Global     => null,
   Import     => True,
   Convention => C,
   External_Name => "compute_fletcher_checksum";
```
```

The C version of this function takes an array of characters and does not modify that array as evidenced by the const in the declaration of the buffer parameter in the C header file. Package Interfaces.C contains a declaration of an unconstrained array type holding C-style characters. Thus, the first parameter of the function is of this type and has mode *in*. The Ada compiler will pass the actual parameter by its address as expected by the C function.