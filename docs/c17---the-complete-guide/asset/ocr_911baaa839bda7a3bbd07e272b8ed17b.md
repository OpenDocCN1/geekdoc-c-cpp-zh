# 8.9 Preprocessor Condition __has_include

C++17 extends the preprocessor to allow you to check whether a specific header file could be included. For example:

```
#if __has_include(<filesystem>)
#   include <filesystem>
#   define HAS_FILESYSTEM 1
#elif __has_include(<experimental/filesystem>)
#   include <experimental/filesystem>
#   define HAS_FILESYSTEM 1
#   define FILESYSTEM_IS_EXPERIMENTAL 1
#elif __has_include("filesystem.hpp")
#   include "filesystem.hpp"
#   define HAS_FILESYSTEM 1
#   define FILESYSTEM_IS_EXPERIMENTAL 1
#else
#   define HAS_FILESYSTEM 0
#endif
```

The conditions inside __has_include(...) evaluate to 1 (true) if a corresponding #include command would be valid. Nothing else matters (e.g., the answer does not depend on whether the file was already included).

Furthermore, the fact that the file exists does not prove that it has the expected contents. It might be empty or invalid.

__has_include is a pure preprocessor feature. Using __has_include as condition in source code is not possible:

```
if (__has_include(<filesystem>)) {  // ERROR
}
```

# 8.10 Afternotes

Nested namespace definitions were first proposed in 2003 by Jon Jagger in http://wg21.link/n1524. Robert Kawulak introduced a new proposal in 2014 in http://wg21.link/n4026. The finally accepted wording was formulated by Robert Kawulak and Andrew Tomazos in http://wg21.link/n4230.

The refined expression evaluation order was first proposed by Gabriel Dos Reis, Herb Sutter, and Jonathan Caves in http://wg21.link/n4228. The finally accepted wording was formulated by Gabriel Dos Reis, Herb Sutter, and Jonathan Caves in http://wg21.link/p0145r3.

Relaxed enum initialization was first proposed by Gabriel Dos Reis in http://wg21.link/p0138r0. The finally accepted wording was formulated by Gabriel Dos Reis in http://wg21.link/p0138r2.

Fixing list initialization with auto was first proposed by Ville Voutilainen in http://wg21.link/n3681 and http://wg21.link/3912. The final fix for list initialization with auto was proposed by James Dennett in http://wg21.link/n3681.