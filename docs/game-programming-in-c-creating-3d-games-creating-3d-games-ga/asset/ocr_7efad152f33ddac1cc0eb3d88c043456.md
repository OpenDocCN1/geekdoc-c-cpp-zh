```
delete[] mArray;
}
```

If you add this destructor, when `scores` goes out of scope, the destructor deallocates `mArray`, eliminating the memory leak.

# The Copy Constructor

The **copy constructor** is a special constructor that creates an object as a copy of another object of the same type. For example, suppose you declare the following `Complex` object:

Click here to view code image

```
Complex c1 = Complex(5.0f, 3.5f);
```

You could then instantiate a second instance of `Complex` as a copy of `c1`:

```
Complex c2(c1);
```

In most cases, C++ provides a copy constructor implementation if the programmer doesn’t declare one. This default copy constructor directly copies all member data from the original object to the new object. For `Complex`, this works perfectly fine; for example, it means that `c2.mReal` and `c2.mImaginary` directly