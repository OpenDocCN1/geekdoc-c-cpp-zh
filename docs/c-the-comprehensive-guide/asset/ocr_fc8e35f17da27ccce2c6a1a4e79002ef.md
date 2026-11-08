+   - **Exception** `bad_alloc`
+   
+     Memory was not allocated; the exception leaves the constructor. Thus, the buffer is considered not created, and no allocated resources are left behind. Because the object was not created, the destructor will not be called under any circumstances—even if data is uninitialized and thus a `delete[]` would be extremely dangerous. It never occurs.

The methods removed with = delete ensure that the buffer is not accidentally copied and then the entire internal data structure is freed multiple times: another reason to use unique_ptr.

# 17.2.2  Owning Raw Pointers

In complex object hierarchies, you must not forget that you also need to be prepared for the initialization of object variables (*member variables*) to fail with an exception. Even if you do not handle and swallow them with catch, but actually want to let the exception pass through, you may need to undo any previous initializations before the exception leaves the current constructor.

Unlike the preceding Buffer class, things are not so simple with StereoImage.

```
```cpp
// https://godbolt.org/z/TK3vTv1EM
struct StereoImage {
    Image *left, *right;
    StereoImage()
      : left(new Image)
      , right(new Image) // Danger!
    { }
    ~StereoImage() {
        delete left;
        delete right;
    }
};
```
```

**Listing 17.6** If “right” throws an exception, a leak occurs with “left”.

If the creation of right fails with an exception here, the memory already allocated for left would not be released. Because the constructor was exited with an exception, the StereoImage is considered not created, and its destructor will not be called. The compiler could undo the successful initialization of left by calling its destructor, but this is a raw pointer without a destructor! Another mechanism is needed—a catch with a rethrow or something other than a raw pointer for the fields of StereoImage.

The following listing provides one example (among many) of how you can avoid this vulnerability.