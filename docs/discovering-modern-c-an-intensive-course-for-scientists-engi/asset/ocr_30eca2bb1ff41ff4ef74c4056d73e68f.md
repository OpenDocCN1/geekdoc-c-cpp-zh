Each entry of our container can be called like a function:

```
for (auto& f : functions)
    cout << "f(6, 3) = " << f(6, 3) << endl;
```

yielding the expected output:

```
f(6, 3) = 9
f(6, 3) = 3
f(6, 3) = 18
f(6, 3) = 216
f(6, 3) = 1
f(6, 3) = 2
f(6, 3) = 2
```

Needless to say, this function wrapper is preferable to function pointers in terms of flexibility and clarity (which we pay for with some overhead).

# 4.4.3 Reference Wrapper

Assume we want to create a list of vectors or matrices—possibly large ones. In addition, suppose that some entries appear multiple times. Therefore, we don't want to store the actual vectors or matrices. We could create a container of pointers, but we want to avoid all the danger related to them (§1.8.2).

Unfortunately, we cannot create a container of references:

```
vector<vector<int>> vv; // Error
```

C++11 provides for this purpose a reference-like type called reference_wrapper that can be included with the header <functional>:

```
vector<reference_wrapper<vector<int> >> vv;
```

The vectors can be inserted:

```
vector<int> v1= {2, 3, 4}, v2= {5, 6}, v3= {7, 8};
vv.push_back(v1);
vv.push_back(v2);
vv.push_back(v3);
vv.push_back(v2);
vv.push_back(v1);
```

They are implicitly converted into reference wrappers (reference_wrapper<T> contains a constructor for T& that is not explicit).

The class contains a method get to get a reference to the actual object so that we can, for instance, print our vector:

```
for (const auto& vr : vv) {
    copy(begin(vr.get()), end(vr.get()),
         ostream_iterator<int>(cout, " "));
    cout << endl;
}
```