# 20.4 Filesystem Operations

| Call | Effect |
|---|---|
| `read_symlink(symlink)` | Yields the file that an existing symbolic link refers to |
| `absolute(p)` | Yields existing p as absolute path (not following symbolic links) |
| `canonical(p)` | Yields existing p as absolute path (following symbolic links) |
| `weakly_canonical(p)` | Yields p as absolute path (following symbolic links) |
| `relative(p)` | Yields relative (or empty) path from current directory to p |
| `relative(p, base)` | Yields relative (or empty) path from base to p |
| `proximate(p)` | Yields relative (or absolute) path from current directory to p |
| `proximate(p, base)` | Yields relative (or absolute) path from base to p |

*Table 20.18. Filesystem Path Conversions*

Note that these functions have different behavior regarding whether the file(s) must exist, whether they normalize, and whether they follow symbolic links. Table *Filesystem Path Conversion Attributes* gives an overview of what the functions require and how they perform.

| Call | Must Exist | Normalizes | Follows Symbolic Links |
|---|---|---|---|
| `read_symlink()` | Yes | Yes | Once |
| `absolute()` | No | Yes | No |
| `canonical()` | Yes | Yes | All |
| `weakly_canonical()` | No | Yes | All |
| `relative()` | No | Yes | All |
| `proximate()` | No | Yes | All |

*Table 20.19. Filesystem Path Conversion Attributes*

The following function demonstrates the use and effect of most of these operations when dealing with symbolic links:

```
*filesystem/symlink.hpp*

```cpp
#include <filesystem>
#include <iostream>

void testSymLink(std::filesystem::path top)
{
    top = absolute(top);       // use absolute paths as we change current path
    create_directory(top);     // make sure top exists
    current_path(top);         // so that we can change the directory to it
    std::cout << std::filesystem::current_path() << '\n';  // print path of top

    // define our sub-directories (without creating them):
    std::filesystem::path px{top / "a/x"};
    std::filesystem::path py{top / "a/y"};
```

```