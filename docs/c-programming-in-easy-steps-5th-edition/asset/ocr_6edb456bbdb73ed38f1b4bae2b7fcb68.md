“exception”, from which other classes are derived, categorizing common exceptions.

Each of the exception classes are listed in the table below, illustrating their relationship and describing their exception type:

| Exception class: | Description: |
|---|---|
| exception | General exception |
| ├─ bad_alloc | – failure allocating storage |
| ├─ bad_cast | – failure casting data type |
| ├─ bad_typeid | – failure referencing typeid |
| ├─ logic_error | Logic exception |
| │  ├─ domain_error | – invalid domain |
| │  ├─ invalid_argument | – invalid argument in call |
| │  ├─ length_error | – invalid length for container |
| │  └─ out_of_range | – invalid element range |
| └─ runtime_error | Runtime exception |
|    ├─ range_error | – invalid range request |
|    └─ overflow_error | – invalid arithmetic request |

![](bbox=[0.1, 0.325, 0.21, 0.4])

The `cout` function sends data to standard output, whereas the `cerr` function sends error data to standard error output. These are simply two different data streams.

When the `<stdexcept>` library is made available to a program, by adding an `#include <stdexcept>` preprocessor directive, the exception classes can be used to identify the type of exception thrown to a `catch` block.

The specific exception class name can appear, in place of the general `exception` type, within the `catch` block’s parentheses.

![](bbox=[0.1, 0.56, 0.21, 0.645])

The example described here demonstrates the use of *standard exceptions*.

Multiple `catch` blocks can be used in succession, much like `case` statements in a `switch` block, to handle several types of exception.

Additionally, exceptions can be produced manually by the `throw` keyword. This can be used to create any of the `logic_error` and `runtime_error` exceptions in the table above. Optionally, a custom error message can be specified for manual exceptions, which can be retrieved by its `what()` function.