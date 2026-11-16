```
});
/** If an %exception is thrown which is not listed in a function's
 * %exception specification, one of these may be thrown. */
class bad_exception : public exception
{
public:
  bad_exception() _GLIBCXX_USE_NOEXCEPT { }
  // This declaration is not useless:
  // http://gcc.gnu.org/onlinedocs/gcc-3.0.2/gcc_6.html#SEC118
  virtual ~bad_exception() _GLIBCXX_USE_NOEXCEPT;
  // See comment in eh_exception.cc.
  virtual const char* what() const _GLIBCXX_USE_NOEXCEPT;
};
```

These are:

| Exception | Description |
|---|---|
| bad_alloc | thrown by new on allocation failure |
| bad_cast | thrown by dynamic_cast when fails with a referenced type |
| bad_exception | thrown when an exception type doesn't match any catch |
| bad_typeid | thrown by typeid |
| ios_base::failure | failure thrown by functions in the iostream library |

Since bad_alloc is derived from the standard base class exception, we can handle that same exception by catching references to the exception class, same with others.

Consider the following program:

```
#include <iostream>
#include <exception>
using namespace std;
```