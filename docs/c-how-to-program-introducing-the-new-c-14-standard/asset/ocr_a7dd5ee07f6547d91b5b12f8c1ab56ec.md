# 13.5 Unformatted I/O Using `read`, `write` and `gcount`

Unformatted input/output is performed using `istream`'s `read` and `ostream`'s `write` member functions, respectively—`read` inputs bytes to a built-in array of `char`s in memory; `write` outputs bytes from a built-in array of `char`s. These bytes are *not formatted* in any way. They’re input or output simply as raw bytes. For example, the call

```
```cpp
char buffer[] {"HAPPY BIRTHDAY"};
cout.write(buffer, 10);
```
```

outputs the first 10 bytes of `buffer` (including null characters, if any, that would cause output with `cout` and `<<` to terminate). The call

```
```cpp
cout.write("ABCDEFGHIJKLMNOPQRSTUVWXYZ", 10);
```
```

displays the first 10 characters of the alphabet.