```
auto some_function(int x)
{
    // ...
    Number auto y = fct(x); // an error unless fct(x) returns a Number
    return y;
    // ...
}
```

语义世