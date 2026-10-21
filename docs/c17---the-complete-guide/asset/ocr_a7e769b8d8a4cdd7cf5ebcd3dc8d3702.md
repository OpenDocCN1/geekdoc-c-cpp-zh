| Memory Resource | Behavior |
|---|---|
| get_default_resource() | Yields a pointer to the current default memory resource |
| set_default_resource(memresPtr) | Sets the default memory resource (passing a pointer) and yields a pointer to the previous one |

Table 29.2. Operations for the Default Memory Resource

with std::pmr::set_default_resource(). This resource is used as the default in any scope until the next call of std::pmr::set_default_resource() is performed. For example:

```
static std::pmr::synchronized_pool_resource myPool;
```

```
// set myPool as new default memory resource:
std::pmr::memory_resource* old = std::pmr::set_default_resource(&myPool);
...
// restore old default memory resource as default:
std::pmr::set_default_resource(old);
```

If you create a custom memory resource in your program and use it as the default resource, it is a good approach to create it as a static object before anything else in main():

```
int main()
{
    static std::pmr::synchronized_pool_resource myPool;
    ...
}
```

Alternatively, provide a global function that returns your resource as a static object:

```
memory_resource* myResource()
{
    static std::pmr::synchronized_pool_resource myPool;
    return &myPool;
}
```

The return type memory_resource is the base class of all memory resources.

Note that a previous default resource might still be used even when it has been replaced. Unless you know (and can ensure) that this is not the case, which means that no static objects are created using the resource, you should have your resource live as long as possible (again, ideally creating it right at the beginning of main() so that it is destroyed last).³