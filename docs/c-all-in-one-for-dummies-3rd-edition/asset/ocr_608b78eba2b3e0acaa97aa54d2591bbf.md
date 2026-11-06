# Adaptors

Adaptors perform conversions of a sort. They make it possible to adapt one kind of data to another. In some cases, adaptors perform data conversion, such as negating numbers. The Adaptors category includes one function, `ptr_fun()`, which is explained in the “Functors” section of the chapter. In addition, the Adaptors category includes the types shown in the following table:

|  |  |  |
|---|---|---|
| `back_insert_iterator` | `binary_compose` | `binary_negate` |
| `binder1st` | `binder2nd` | `front_insert_iterator` |
| `insert_iterator` | `mem_fun1_ref_t` | `mem_fun1_t` |
| `mem_fun_ref_t` | `mem_fun_t` | `pointer_to_binary_function` |
| `pointer_to_unary_function` | `priority_queue` | `queue` |
| `raw_storage_iterator` | `reverse_bidirectional_iterator` | `reverse_iterator` |
| `sequence_buffer` | `stack` | `unary_compose` |
| `unary_negate` |  |  |

# Allocators

*Allocators* manage resources, normally memory. In most cases, you won’t ever need to use the members of the Allocators category. For example, you normally create new objects using the new operator. The new operator allocates memory for the object and then creates it by calling the object’s constructor. In rare cases, such as when you want to implement a form of object pooling, you may want to separate the memory allocation process from the construction process. In this case, you call `construct()` to perform the actual task of constructing the object based on its class definition. The Allocators category has the following functions:

|  |  |  |
|---|---|---|
| `construct` | `destroy` | `get_temporary_buffer` |
| `return_temporary_buffer` | `uninitialized_copy` | `uninitialized_copy_n` |
| `uninitialized_fill` | `uninitialized_fill_n` |  |