```
```cpp
cout << fixed << showpoint << setprecision(1);

for (size_t i(0); i < size; ++i) {
    cout << numbers[i] << ' ';
}
```
```

D.

```
```cpp
nPtr = numbers;
nPtr = &numbers[0];
```
```

E.

```
```cpp
cout << fixed << showpoint << setprecision(1);

for (size_t j(0); j < size; ++j) {
    cout << *(nPtr + j) << ' ';
}
```
```

F.

```
```cpp
cout << fixed << showpoint << setprecision(1);

for (size_t k(0); k < size; ++k) {
    cout << *(numbers + k) << ' ';
}
```
```