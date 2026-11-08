# # L-values and R-values

It wouldn’t be C++ if we didn’t talk about L-values and R-values at least briefly. L-values are so called because they traditionally appear on the left side of an equal sign. In other words, they are values that can be assigned to—those which will survive the evaluation of the current expression. The most familiar type of L-value is a variable, but it also includes the result of calling a function that returns an L-value reference.

R-values traditionally appear on the right side of the equation or, perhaps more accurately, they are values that could not appear on the left. They are things such as constants, or the result of evaluating an equation. For example, a + b where a and b might be L-values, but the result of adding them together is an R-value, or the return value of a function that returns anything other than void or an L-value reference.

# ## References

References act just like non-pointer variables. Once a reference is initialized, it cannot refer to another object. You also must initialize a reference where you declare it. If your functions take references rather than objects, you will not incur the cost of a copy construction. Since the reference refers to the object, changes to it are changes to the object itself.

Just like pointers, you can also have a const reference. Unless you need to modify the object, you should use const references since they provide compiler checks to ensure that you aren’t mutating the object when you think you aren’t.

There are two types of references: L-value references and R-value references. An L-value reference is marked by an && appended to the type name (e.g., SomeClass&), whereas an R-value reference is marked by an && appended to the type name (e.g., SomeClass&&). For the most part, they act the same; the main difference is that R-value references is extremely important to move semantics.

# ## Pointer and Reference Sample

The following sample shows pointer and reference usage with explanations in the comments.

**Sample: PointerSample\PointerSample.cpp**

```
```cpp
#include <memory>
// See the comment to the first use of assert() in _pmain below.
//#define NDEBUG 1
#include <cassert>
#include "../pchar.h"

using namespace std;

void SetValueToZero(int& value)
{
        value = 0;
}

void SetValueToZero(int* value)
{
        *value = 0;
}

int _pmain(int /*argc*/, _pchar* /*argv*/[])
{
        int value = 0;
```
```