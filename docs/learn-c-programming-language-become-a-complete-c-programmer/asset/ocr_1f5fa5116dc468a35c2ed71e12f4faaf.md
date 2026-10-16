```
```cpp
cout << d1.count() << ‘\n’; // 7
cout << d2.count() << ‘\n’; // 7e+009
if (d1!=d2) cerr<<“insane!”;
```
```

Here, **d1** and **d2** are equal but report very different **count()** values. Care is taken to avoid truncation or loss of precision during initialization (even if the **{}** notation is not used). For example:

```
```cpp
duration<int, milli> d {3}; // OK
duration<int, milli> d {3.5}; // error: 3.5 to int is narrowing

duration<int, milli> ms {3};
duration<int, micro> us {ms}; // OK
duration<int, milli> ms2 {us}; // error: we could lose many microseconds
```
```

The standard library provides meaningful arithmetic operations on **durations**:

**duration<Rep,Period> (continued) (§iso.20.11.5)**
**r** is a **Rep**; arithmetic is done in the **common_type** of the representations

```
```cpp
++d    ++d.r
d++    duration{d.r++}
--d    --d.r
d--    duration{d.r--}
+d     d
-d     duration{-d.r}
d+=d2  d.r+=d2.r
d-=d2  d.r-=d2.r
d%=d2  d.r%=d2.r.count()
d%=r   d.r+=r
d*=r   d.r+=r
d/=r   d.r+=r
```
```

The **period** is a unit system, so there is no **=** or **+=** taking a plain value. Allowing that would be like allowing the addition of **5** of an unknown SI unit to a length in meters. Consider:

```
```cpp
duration<long long,milli> d1 {7}; // 7 milliseconds
d1 += 5; // error

duration<int,ratio<1,1>> d2 {7}; // 7 seconds
d2 = 5; // error
d2 += 5; // error
```
```

What would **5** mean here? **5** seconds? **5** milliseconds? Something else? If you know what you mean, be explicit about it. For example:

```
```cpp
d1 += duration<long long,milli>{5}; // OK: milliseconds
d3 += decltype(d2){5}; // OK: seconds
```
```

Arithmetic involving **durations** with different representations is allowed as long as the combination makes sense (§35.2.4):

**duration<Rep,Period> (continued) (§iso.20.11.5)**
**r** is a **Rep**; arithmetic is done in the **common_type** of the representations