```
// ===== t.hpp:
// common header (inclusion model)
template<typename T>
class S {
    public:
        void f();
};

template<typename T>
void S::f()    // member definition
{
}

void helper(S<int>*);

// ===== a.cpp:
#include "t.hpp"

void helper(S<int>* s)
{
    s->f();    // #1 first point of instantiation of S::f
}

// ===== b.cpp:
#include "t.hpp"

int main()
{
    S<int> s;
    helper(&s);
    s.f();    // #2 second point of instantiation of S::f
}
```