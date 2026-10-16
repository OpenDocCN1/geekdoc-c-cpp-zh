```
swap(i1, i2);
cout << i1 << ' ' << i2 << endl;

double d1 = 33.3,
d2 = 44.4;
swap(d1, d2);
cout << d1 << ' ' << d2 << endl;

string s1 = "Hi",
s2 = "Ho";
swap(s1, s2);
cout << s1 << ' ' << s2 << endl;
}
```

When the compiler encounters the first call to swap(),

```
swap(i1, i2);
```

in which the two arguments i1 and i2 are of type int, it uses the pattern given by our template to generate a new definition of swap() in which the type parameter Item is replaced by int:

```
inline void swap(int & first, int & second)
{
    int temporary = first;
    first = second;
    second = temporary;
}
```

When it reaches the second call,

```
swap(d1, d2);
```

where the two arguments d1 and d2 are of type double, the compiler will use the same pattern to generate a second definition of swap() in which the type parameter Item is replaced by double:

```
inline void swap(double & first, double & second)
{
    double temporary = first;
    first = second;
    second = temporary;
}
```

When the compiler reaches the final call,

```
swap(s1, s2);
```