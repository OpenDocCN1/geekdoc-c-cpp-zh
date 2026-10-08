```
```
double* p = ad;            // error: no implicit conversion to pointer
double* q = ad.data();     // OK: explicit conversion
```
```

```
```
template<typename C> void printout(const C& c)  // function template
{
    for (int i = 0; i<c.size(); ++i) cout << c[i] <<'\n';
}
```
```

This **printout()** can be called by an **array** as well as a **vector**:

```
```
printout(ad);                  // call with array
vector<int> vi;
// ...
printout(vi);                  // call with vector
```
```

This is a simple example of generic programming applied to data access. It works because the interface used for **array** and **vector** (**size()** and subscripting) is the same. Chapters 20 and 21 will explore this style of programming in some detail.

# ### 19.3.6 Template argument deduction

For a class template, you specify the template arguments when you create an ob- ject of some specific class. For example:

```
```
array<char,1024> buf;           // for buf, T is char and N is 1024
array<double,10> b2;           // for b2, T is double and N is 10
```
```

For a function template, the compiler usually deduces the template arguments from the function arguments. For example:

```
```
template<class T, int N> void fill(array<T,N>& b, const T& val)
{
    for (int i = 0; i<N; ++i) b[i] = val;
}

void f()
{
    fill(buf,'x');             // for fill(), T is char and N is 1024
                               // because that's what buf has
    fill(b2,0.0);              // for fill(), T is double and N is 10
                               // because that's what b2 has
}
```
```