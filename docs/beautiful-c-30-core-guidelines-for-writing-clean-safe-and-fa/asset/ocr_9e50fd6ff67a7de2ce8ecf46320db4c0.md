Rather than use flow control to ensure code is executed, it is safer to make use of the idiom known as Resource Acquisition Is Initialization, or RAII. In this case, we bun-dle the acquire and release functions with the handle into a single struct:

Click here to view code image

```
```
int display(int ID)
{
    struct resource {
        resource(int h_) : h(h_) {}
        ~resource() { release_handle(h); }
        operator int() { return h; }

    private:
        int h;
    };

    resource r(get_handle_to_resource(ID));
    if (r == 0) {
        return 0;
    }
    auto j = manipulate_resource(r);
    if (j < 0) {
        return 0;
    }
    auto k = supply_resource_to_system(r, j);
    if (k < 0) {
        return 0;
    }
    display_resource(r);
    return 1;
}
```
```