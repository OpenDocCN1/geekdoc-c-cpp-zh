Namespace aliases also allow a user to refer to “the library” and have a single declaration defining what library that really is. For example:

```
namespace Lib = Foundation_library_v2r11;
// …
Lib::set s;
Lib::String s5 = “Sibelius”;
```

This can immensely simplify the task of replacing one version of a library with another. By using **Lib** rather than **Foundation_library_v2r11** directly, you can update to version “v3r02” by changing the initialization of the alias **Lib** and recompiling. The recompile will catch source-level incompatibilities. On the other hand, overuse of aliases (of any kind) can lead to confusion.

# 14.4.3 Namespace Composition

Often, we want to compose an interface out of existing interfaces. For example:

```
namespace His_string {
class String { /* … */ };
String operator+(const String&, const String&);
String operator+(const String&, const char*);
void fill(char);
// …
}
namespace Her_vector {
template<class T>
class Vector { /* … */ }; // …

namespace My_lib {
using namespace His_string;
using namespace Her_vector;
void my_fct(String&);
}
```

Given this, we can now write the program in terms of **My_lib**:

```
void f()
{
My_lib::String s = “Byron”; // finds My_lib::His_string::String // …
}

using namespace My_lib;

void g(Vector<String>& vs) {
// …
my_fct(vs[5]);
// …
}
```