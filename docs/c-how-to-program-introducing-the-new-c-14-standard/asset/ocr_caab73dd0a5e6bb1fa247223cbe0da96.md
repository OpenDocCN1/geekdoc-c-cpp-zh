# 14.8.1 Writing Bytes with `ostream`  
Member Function `write`

Writing the integer `number` to a file using the statement

```
```cpp
outFile << number;
```
```

for a four-byte integer could output 1 to 11 bytes—up to 10 digits for a
number in the range −2,147,483,647 to 2,147,483,647, plus a sign for
a negative number. Instead, we can use the statement

```
```cpp
outFile.write(
    reinterpret_cast<const char*>(&number), sizeof(number));
```
```

which always writes in *binary* the four bytes used that represent the
integer `number`. Function `write` treats its first argument as a group of
bytes by viewing the object in memory as a `const char*`, which is a
pointer to a byte (recall that a `char` is 1 byte). Starting from that
location, function `write` outputs the number of bytes specified by its