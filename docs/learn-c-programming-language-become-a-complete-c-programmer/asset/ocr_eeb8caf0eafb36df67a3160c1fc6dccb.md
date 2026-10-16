The == looks more or less like all ==s. It is defined for values of the same Units only:

```
template<typename U>
bool operator==(Quantity<U> x, Quantity<U> y)
{
return x.val==y.val; }
```

```
template<typename U>
bool operator!=(Quantity<U> x, Quantity<U> y) {
return x.val!=y.val;
}
```

Note that I pass Quantity by value. At run time, they are represented as doubles. The output functions just do conventional character manipulation:

```
string suffix(int u, const char*x) // helper function
{
string suf;
if (u) {
suf += x;
if (1<u) suf += ‘0’+u;
if (u<0) {
suf += ‘–’; suf += ‘0’–u;
}
}
return suf;
}
```

```
template<typename U>
ostream& operator<<(ostream& os, Quantity<U> v) {
return os << v.val << suffix(U::m,"m") << suffix(U::kg,"kg") << suffix(U::s,"s"); }
```

Finally, we can write:

```
auto distance = 10_m;
auto time = 20_s;
auto speed = distance/time;
```

```
// 10 meters
// 20 seconds
// .5 m/s (meters per second)
```

```
if (speed == 20)
// ...
if (speed == distance) // ...
if (speed == 10_m/20_s) // ...
// error :20 is dimensionless
```