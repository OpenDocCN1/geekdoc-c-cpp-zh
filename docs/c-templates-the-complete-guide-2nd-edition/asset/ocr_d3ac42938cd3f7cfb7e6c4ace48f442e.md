what is saved by reusing them. A key concept to this approach is that a precompiled header for a more stable layer can be reused to improve the precompilation time of a less stable header. For example, suppose that in addition to our std.hpp header (which we have precompiled), we also define a core.hpp header that includes additional facilities that are specific to our project but nonetheless achieve a certain level of stability:

```
#include "std.hpp"
#include "core_data.hpp"
#include "core_algos.hpp"
```

...
Because this file starts with #include "std.hpp", the compiler can load the associated precom-piled header and continue with the next line without recompiling all the standard headers. When the file is completely processed, a new precompiled header can be produced. Applications can then use #include "core.hpp" to provide access quickly to large amounts of functionality because the compiler can load the latter precompiled header.

# 9.4 Decoding the Error Novel

Ordinary compilation errors are normally quite succinct and to the point. For example, when a compiler says “class X has no member ‘fun’,” it usually isn’t too hard to figure out what is wrong in our code (e.g., we might have mistyped run as fun). Not so with templates. Let’s look at some examples.

# Simple Type Mismatch

Consider the following relatively simple example using the C++ standard library: Click here to view code image

basics/errornovel1.cpp

```
#include <string>
#include <map>
#include <algorithm>
int main()
{
std::map<std::string,double> coll;
"""
// find the first nonempty string in coll:
auto pos = std::find_if (coll.begin(), coll.end(),
```