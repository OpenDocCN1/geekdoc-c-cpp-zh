then that would be a different matter. You do not own w, so it is not yours to pass around. The size function may take a copy of w and cache it for later use, so unless you are certain of the implementation of that function and you are also in charge of how it might change, passing w is unsafe. If the object w points to is destroyed later, then that copy of w will be pointing to nothing and dereferencing it will be poten-tially disastrous.

This function takes an object by pointer and then passes it to another function. This implies ownership, which is not conveyed in the function signature. Do not transfer ownership by a raw pointer.

The correct way to implement this function is:

Click here to view code image

```
size_t measure_widget(std::shared_ptr<Widget> w) {
    return size(w);
}
```

You are now giving the size() function an interest in the std::shared_ptr. If the call-ing function subsequently destroys w, the size() function can still retain a copy.

# Using unadorned reference semantics

A raw pointer is not the only way to pass an object by reference rather than by value. You can also achieve this using a reference. Using a reference is the preferred mecha-nism of passing by reference. Consider this version of measure_widget:

Click here to view code image

```
size_t measure_widget(Widget& w) {
    return w.size(); // (References cannot be null
without evil intent)
}
```