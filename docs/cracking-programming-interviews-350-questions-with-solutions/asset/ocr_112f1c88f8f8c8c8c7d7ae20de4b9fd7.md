```
```cpp
int i;
}

namespace B
{
    using namespace Z;

    void f(char);

    int i;
}

namespace AB
{
    using namespace A;
    using namespace B;

    void g();
}
```
```

What happens with the code fragments as follows:

+   1. `AB::g();`

+   2. `AB::f(1);`

+   3. `AB::f('e');`

+   4. `AB::x++;`

+   5. `AB::i++;`