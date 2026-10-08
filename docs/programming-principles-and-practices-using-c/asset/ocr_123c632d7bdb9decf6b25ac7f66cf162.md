```
```cpp
// ...
int x1 = find(v1,2);    // find()’s T is int
int x2 = find(v2,2);    // find()’s T is double
```
```

It is possible to define a template function for which it is not possible to deduce its template arguments from its function arguments. In that case we must specify the missing template arguments explicitly (exactly as for class templates). For example:

```
```cpp
template<class T, class U> T* make(const U& u) { return new T(u); }
int* pi = make<int>(2);
Node* pn = make<Node>(make_pair("hello",17));
```
```

This works if **Node** can be initialized by a **pair<**const char * **,int>** (§B.6.3). Only trailing template arguments can be left out of an explicit argument specialization (to be deduced).

# ### A.13.2 Template instantiation

A version of a template for a specific set of template arguments is called a *specialization*. The process of generating specializations from a template and a set of arguments is called *template instantiation*. Usually, the compiler generates a specialization from a template and a set of template arguments, but the programmer can also define a specific specialization. This is usually done when a general template is unsuitable for a particular set of arguments. For example:

```
```cpp
template<class T> struct Compare {           // general compare
    bool operator()(const T& a, const T& b) const
    {
        return a<b;
    }
};

template<> struct Compare<const char*> {     // compare C-style strings
    bool operator()(const char* a, const char* b) const
    {
        return strcmp(a,b)<0;
    }
};

Compare<int> c2;                              // general compare
Compare<const char*> c;                       // C-style string compare
```
```