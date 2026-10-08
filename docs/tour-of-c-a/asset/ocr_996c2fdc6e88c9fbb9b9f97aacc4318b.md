of our own user-defined types. For example:

Click here to view code image

```
struct Reading {
    int location();
    int temperature();
    int humidity();
    int air_pressure();
    //...
}
int average_temp(vector<Reading> readings) {
    if (readings.size()==0) throw No_readings();
    double s = 0;
    for (int x : views::elements<1>(readings))
        s += x;
    return s/readings.size();
}
```

# 14.3 Generators

Often, a range needs to be generated on the fly. The standard library provides a few simple generators (aka factories) for that:

| Range factories <ranges> |
| v is a view; x of the element type T; is an an istream |
| v=empty_view<T>() | v is an empty range of type T (had had any) |
| v=single_view(x) | v is a range of the one element x |
| v=iota_view(x) | v is a infinite range of elements: x, x+1, x+2, ...
incrementing is done using ++ |
| v=iota_view(x,y) | v is a range of n elements: x, x+1, ..., y-1
incrementing is done using ++ |
| v=istream_view<T>(is) | v is the range obtained by calling >> to T on is |

The Iota views are useful for generating simple sequences. For example:

Click here to view code image

```
for (int x : iota_view<42,52)) // 42 43 44 45 46 47 48 49 50 51
cout << x << "\n";
```

The istream_view gives a simple example of using istreams in range-for loops:

Click here to view code image

```
for (auto x : istream_view<complex<double>>(cin))
cout << x << "\n";
```