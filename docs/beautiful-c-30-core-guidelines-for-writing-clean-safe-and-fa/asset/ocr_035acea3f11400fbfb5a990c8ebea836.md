```
using flump_fn_ptr = void(*)(int);

struct flumper {
    flump_fn_ptr flump;
    ...
};

void flump_fn(int);

void fn()
{
    flumper fl { flump_fn; }
    fl.flump(7);
}
```