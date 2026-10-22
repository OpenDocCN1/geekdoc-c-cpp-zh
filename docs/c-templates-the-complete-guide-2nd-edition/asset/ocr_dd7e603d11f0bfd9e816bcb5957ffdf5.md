```
```cpp
extern int count;                          // #1

int lookup_example(int count)              // #2
{
    if (count < 0) {
        int count = 1;                      // #3
        lookup_example(count);              // unqualified count refers to #3
    }
    return count + ::count;                 // the first (unqualified) count refers to #2;
                                            // the second (qualified) count refers to #1
}
```
```