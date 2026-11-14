```
```cpp
void self_observing_function()
{
    static int counter= 0;     // only executed once
    ++counter;
    cout << "I was called " << counter << " times.\n";
    ...
}
```
```