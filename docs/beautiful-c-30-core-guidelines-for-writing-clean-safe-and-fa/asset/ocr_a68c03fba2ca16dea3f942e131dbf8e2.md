Note that this code is not signaling errors by throwing exceptions but by using multi-ple return statements with different values to signal success. If this were a C++ library rather than a C library, we might expect the functions to throw an error rather than return. What would our example look like then?

Click here to view code image

```
```cpp
void display(int ID)
{
    struct resource {
        resource(int h_) : h(h_) {}
        ~resource() { release_handle(h); }
        operator int() { return h; }

    private:
        int h;
    };

    resource r(get_handle_to_resource(ID));
    auto j = manipulate_resource(r);
    supply_resource_to_system(r, j);
    display_resource(r);
}
```
```

Of course, we might also expect the functions to take user-defined types rather than ints, but please let that pass for the sake of this example.

Now we have no explicit return at all. This is to be expected; after all, this func-tion simply does something, not even signaling success or failure. With exceptions used to signal failure there is no need for a return statement: the code assumes suc-cess and invisibly throws if it fails. It doesn’t calculate a value and return it.

This struct is so useful it should be pulled out of that function and made available to other users. Indeed, I’ve seen many codebases that interface with C libraries that contain something like this: