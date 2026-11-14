```
```cpp
try {
    A = read_matrix_file("does_not_exist.dat");
} catch (const cannot_open_file& e) {
    cerr << "O my gosh, the file is not there! Please caller help me.\n";
    throw;
}
```
```