![](bbox=[0.04, 0.08, 0.95, 0.4])

# 11.5 DIFFERENCES BETWEEN CLASSES AND STRUCTS

A struct is a simple lightweight alternative to a class. Although structs are basically the same as classes, structs are designed more for the situations where we simply want to group some data together. Structs, therefore, differ significantly from classes in design and implementation. (Classes are discussed in Chapters 12 and 13). Important differences are listed in Table 11.1.

Table 11.1 Class and struct differences

| CATEGORY | CLASSES | STRUCTS |
|---|---|---|
| Data Type | Reference type and therefore stored on the heap | Value type and therefore stored on the stack. Behave like simple data types |
| Inheritance | Support inheritance | Do not support inheritance |
| Default values | Default value of a class type is null | Default value is the value produced by 'zeroing out' the fields of the struct |
| Field initialization | Permit initialization of instance fields | Do not permit initialization of instance fields |
| Constructors | Permit declaration of parameterless constructors | Do not permit declaration of parameterless constructors |
| Destructors | Supported | Not supported |
| Assignment | Assignment copies the reference | Assignment copies the values. |

The fact that structs are value types will affect performance when they are passed as parameters to methods. We can avoid this performance loss by passing structs as ref parameters to methods. In this case, only the address in memory will be passed in, which is as fast as passing in a class.