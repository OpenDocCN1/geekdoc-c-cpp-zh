```
```cpp
for (size_t row{0}; row < a.size(); ++row) {
    for (size_t column{0}; column < a[row].size(); ++column) {
        cout << a[row][column] << ' ';
    }

    cout << endl;
}
```
```

# ## Other Common Two-Dimensional `array` Manipulations

The following `for` statement sets all the elements in row 2 of `array a` in **Fig. 7.16** to zero:

```
```cpp
for (size_t column{0}; column < 4; ++column) {
    a[2][column] = 0;
}
```
```

The `for` statement varies only the second subscript (i.e., the column subscript). The preceding `for` statement is equivalent to the following assignment statements: