```
int& bad()
{
    int x;
    // ...
    return x; // bad: return a reference to the local variable x
}
```