# # Jump functions

`<setjmp.h>`

The **setjmp.h** header is used for controlling low-level calls and provides a means to avoid the normal call and return sequence.

| Function | Description |
|---|---|
| `int setjmp( jmp_buf env )` | Low-level function used in conditional tests to save the environment in the *env* variable, then return zero |
| `void longjmp( jmp_buf env , int value )` | Restores an environment that has been saved in the *env* variable by `setjmp()`, as if `setjmp()` had returned the *value* |