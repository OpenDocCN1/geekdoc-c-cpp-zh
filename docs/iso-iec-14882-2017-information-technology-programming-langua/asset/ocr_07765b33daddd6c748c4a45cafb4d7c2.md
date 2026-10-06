# ISO/IEC 14882:2017(E)

# 20.5.1.2 Headers

[headers]

+   1 Each element of the C++ standard library is declared or defined (as appropriate) in a header.\^{168}
2 The C++ standard library provides the C++ library headers, shown in Table 16.

Table 16 — C++ library headers

| <algorithm> | <future> | <sstream> |
| --- | --- | --- |
| <any> | <initializer_list> | <optional> |
| <array> | <complex> | <system_error> |
| <atomic> | <ostream> | <thread> |
| <bitset> | <queue> | <tuple> |
| <chrono> | <random> | <type_traits> |
| <complexcvt> | <iostream> | <typeindex> |
| <condition> | <regex> | <typeinfo> |
| <condition_variable> | <allocator> | <unordered_map> |
| <deque> | <set> | <unordered_set> |
| <exception> | <list> | <shared_mutex> |
| <execution> | <local> | <utility> |
| <filesystem> | <map> | <valarray> |
| <forward_list> | <memory> | <variant> |
| <fstream> | <memory_resource> | <vector> |
| <functional> | <streambuf> | |
| | <string> | |
| | <mutex> | |
| | <string_view> =

+   3 The facilities of the C standard library are provided in the additional headers shown in Table 17.\^{169}

Table 17 — C++ headers for C facilities

| <cassert> | <cstdio> | <cuchar> |
| --- | --- | --- |
| <complex> | <iso6449> | <stdexcept> |
| <cctype> | <limits> | <stdarg> | <string> |
| <cerrno> | <locale> | <stddb> | <cmath> |
| <cfloat> | <math> | <stddef> | <time> |
| | <setjmp> | <cint> | <cuchar> =

+   4 Except as noted in Clauses 20 through 33 and Annex D, the contents of each header name are the same as that of the corresponding name in the C standard library (Clause 2). In the C++ standard library, the declarations (except defined as macros in C) are within namespace scope (6.3.8) of the standard namespace. It is unspecified whether these names (including any overlaps declared in Clauses 21 through 33 and Annex D) are first declared in the global namespace and then injected into standard namespace using explicit declarations.(170)

+   5 Names which are defined as macros in C shall be defined in the C++ standard library, if a C license allows for such implementation. [Note: The names defined as macros in C include the following: assert, offset, stdarg, va_arg, end, and var. — end node]

+   6 Names header that are defined in C shall be defined in the C++ standard library.\^{170}

> \168} A header is not necessarily a source file, nor are the sequences defined by < and > in headers necessarily valid source file names (19.2).\^{169} It is intentional that there is no C++ header for any of these headers: <statomic.h>, <stdretturn.h>, <threads.h>^{170} This disables the practice, in C, of providing a masking macro in addition to the function prototype. The only way to achieve equivalent inline behavior in C++ is to provide a definition as an inline function.

§ 20.5.1.2 ©/IEC 2017 — All rights reserved 455