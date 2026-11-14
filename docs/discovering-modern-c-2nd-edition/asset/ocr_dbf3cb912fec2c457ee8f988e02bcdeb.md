```
```cpp
int main()
{
    complex c1, c2;
    // set c1
    c1.set_r(3.0);          // Clumsy init
    c1.set_i(2.0);

    // copy c1 to c2
    c2.set_r(c1.get_r());   // Clumsy copy
    c2.set_i(c1.get_i());
    return 0;
}
```
```