```
std::unique_ptr<std::string> source()
{
    static long id{0};

    // create string with new and let ptr own it:
    auto ptr = std::make_unique<std::string>("obj" + std::to_string(++id));
    ...
    return ptr;        // transfer ownership to caller
}

int main()
{
    std::unique_ptr<std::string> p;
    for (int i = 0; i < 10; ++i) {
        p = source();    // p gets ownership of the returned object
                         // (previously returned object of source() is deleted)
        std::cout << *p << '\n';
        ...
    }
} // last-owned object of p is deleted
```

As usual for moved-from types, to pass ownership to a sink function you can only pass it with std::move():

```
std::vector<std::unique_ptr<std::string>> coll;
std::unique_ptr<std::string> up;
...
coll.push_back(up);            // ERROR: copying disabled
coll.push_back(std::move(up)); // OK, moves ownership into new element of coll
```

If you pass a unique pointer to a potential sink function that takes the argument by reference, you do not know whether the ownership was moved. Whether the ownership was moved depends on the implementation of the function. In that case, you can double-check the state with operator bool():

```
std::unique_ptr<std::string> up;
...
sink(std::move(up)); // might move ownership to sink()
if (up) {            // does it still have the ownership?
    ...
}
```

Alternatively, you might ensure that the ownership is gone (resource released):

```
std::unique_ptr<std::string> up;
...
sink(std::move(up)); // might move ownership to sink()
up.reset();          // ensure ownership is gone (resource deleted)
```