library error codes in your project, it is recommended to proceed as follows:

+   - Define an enum with your own error codes.
- Then use make_error_code in your library with these error codes as parameters.
- Create an overload of make_error_category for your error code enum and map your error codes to portable error_category elements there.
- Specialize the template std::error_condition_enum<> with the content true_type so that the standard library knows you support error_category.

The last step, mapping to error_condition, is optional you do not need the coarse granularity in the consuming code:

```
// https://godbolt.org/z/11Tdr6aG1
#include <system_error>
#include <iostream>
using std::error_code; using std::system_category;
namespace myList {
    // custom error codes
    enum class err { LOAD_ERR = 1, UNLOAD_ERR = 2, OTHER_ERR = 3 };
    error_code make_error_code(err ec) {
        switch(ec)
            case err::LOAD_ERR: return error_code((int)ec,
                system_category());
            case err::UNLOAD_ERR: return error_code((int)ec,
                system_category());
            case err::OTHER_ERR: return error_code((int)ec,
                system_category());
        }
    }
    error_code run(int arg) {
        if(arg == 667)
            return make_error_code(err::OTHER_ERR);
        return error_code(); // all good.
    }
}
```