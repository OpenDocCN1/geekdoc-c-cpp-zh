Let’s look at an example demonstrating the wisdom of a single return statement. Assume this function is calling an old C library exporting functions for acquiring, manipulating, and displaying resources based on an integer identifier:

Click here to view code image

```
int display(int ID)
{
    auto h = get_handle_to_resource(ID);
    if (h == 0) {
        return 0;
    }
    auto j = manipulate_resource(h);
    if (j < 0) {
        release_handle(h);
        return 0;
    }
    auto k = supply_resource_to_system(h, j);
    if (k < 0) {
        return 0; /* forgot to release handle */
    }
    display_resource(h);
    release_handle(h);
    return 1;
}
```

In this snippet of code, we see a very common situation: a handle to a resource is acquired and must subsequently be released before the handle falls out of scope. The engineer has forgotten to release the handle at the third return statement. One solu-tion is to have a single return statement, preceded by the release of the handle, thus:

Click here to view code image