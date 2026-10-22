```
```cpp
template<typename T>
void f(T)
{
}
```
```

```
```cpp
// four valid explicit instantiations:
template void f<int>(int);
template void f<>(float);
template void f(long);
template void f(char);
```
```