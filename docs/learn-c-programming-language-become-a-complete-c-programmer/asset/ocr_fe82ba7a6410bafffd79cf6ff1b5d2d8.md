+   <typeindex>
+   <functional>
+   <memory>
+   <scoped_allocator> <ratio>
+   <chrono>
+   <ctime>
+   <iterator>

Type traits §35.4.1 Use a **type_info** as a key or a hash code §35.5.4 Function objects §33.4 Resource management pointers §34.3 Scoped allocators §34.4.4 Compile-time rational arithmetic §35.3 Time utilities §35.2 C-style date and time §43.6 Iterators and iterator support §33.1

Iterators provide the mechanism to make standard algorithms generic (§3.4.2, §33.1.4).

+   <algorithm> <cstdlib>

# Algorithms

General algorithms §32.2
**bsearch()**, **qsort()** §43.7

A typical general algorithm can be applied to any sequence (§3.4.2, §32.2) of any type of element. The C standard library functions **bsearch()** and **qsort()** apply to built-in arrays with elements of types without user-defined copy constructors and destructors only (§12.5).

+   <exception>
+   <stdexcept>
+   <cassert>
+   <cerrno>
+   <system_error>

# Diagnostics

Exception class §30.4.1.1 Standard exceptions §30.4.1.1 Assert macro §30.4.2 C-style error handling §13.1.1.2 System error support §30.4.3

Assertions using exceptions are described in §13.4.

+   <string>
+   <cctype> <cwctype> <cstring> <cwchar> <cstdlib> <cuchar> <regex>

# Strings and Characters

String of T Chapter 36 Character classification §36.2.1 Wide-character classification §36.2.1 C-style string functions §43.4 C-style wide-character string functions §36.2.1 C-style allocation functions §43.5 C-style multibyte characters
Regular expression matching Chapter 37

The **<cstring>** header declares the **strlen()**, **strcpy()**, etc., family of functions. The **<cstdlib>** declares **atof()** and **atoi()** which convert C-style strings to numeric values.

+   <iosfwd>
+   < iostream> <ios>