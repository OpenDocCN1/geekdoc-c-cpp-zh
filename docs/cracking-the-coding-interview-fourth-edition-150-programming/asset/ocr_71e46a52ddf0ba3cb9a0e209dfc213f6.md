# Solutions to Chapter 16 | Low Level

16.5 Write a program to find whether a machine is big endian or little endian.

```
#define BIG_ENDIAN 0
#define LITTLE_ENDIAN 1
int TestByteOrder() {
    short int word = 0x0001;
    char *byte = (char *) &word;
    return (byte[0] ? LITTLE_ENDIAN : BIG_ENDIAN);
}
```