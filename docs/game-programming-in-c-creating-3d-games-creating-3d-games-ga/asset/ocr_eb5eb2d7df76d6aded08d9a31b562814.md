```
for (int i = 0; i < 50; i++)
{
    array[i] = 0;
}
```

> **warning**
> **ARRAYS DON'T BOUND CHECK:** Requesting invalid indices can lead to memory corruption and other errors. Several tools exist to help find bad memory accesses, such as the AddressSanitizer tool available in Xcode.

C++ stores arrays contiguously in memory. This means that the data for index 0 is right next to the data for index 1, which is right next to index 2, and so on. Table A.4 shows an example of a five-element array in memory. Keep in mind that the variable array (without the subscript) references the memory address of index 0 (in this case, 0xF2E0). Because of this, you can pass a single-dimensional array to a function via a pointer.

# Table A.4 An Array in Memory

| Code | Variable | Memory Address | Value |
|---|---|---|---|
| int array[5] = { 2, 4, 6, 8, 10 }; | array[0] | 0xF2E0 | 2 |
| | array[1] | 0xF2E4 | 4 |
| | array[2] | 0xF2E8 | 6 |