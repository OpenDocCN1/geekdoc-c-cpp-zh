These rules lead to the simplest, least error-prone, and most efficient code. By “very small” we mean one or two **ints**, one or two **doubles**, or something like that. If we see an argument passed by non-**const** reference, we must assume that the called function will modify that argument.

That third rule reflects that you have a choice when you want to use a function to change the value of a variable. Consider:

```
```cpp
int incr1(int a) { return a+1; }  // return the new value as the result
void incr2(int& a) { ++a; }        // modify object passed as reference

int x = 7;
x = incr1(x);                      // pretty obvious
incr2(x);                          // pretty obscure
```
```

Why do we ever use non-**const**-reference arguments? Occasionally, they are essential

+   - For manipulating containers (e.g., **vector**) and other large objects
- For functions that change several objects (we can have only one return value)

For example:

```
```cpp
void larger(vector<int>& v1, vector<int>& v2)
    // make each element in v1 the larger of the corresponding
    // elements in v1 and v2;
    // similarly, make each element of v2 the smaller
{
    if (v1.size()!=v2.size()) error("larger(): different sizes");
    for (int i=0; i<v1.size(); ++i)
        if (v1[i]<v2[i])
            swap(v1[i],v2[i]);
}

void f()
{
    vector<int> vx;
    vector<int> vy;
    // read vx and vy from input
    larger(vx,vy);
    // ... .
}
```
```

Using pass-by-reference arguments is the only reasonable choice for a function like **larger**().