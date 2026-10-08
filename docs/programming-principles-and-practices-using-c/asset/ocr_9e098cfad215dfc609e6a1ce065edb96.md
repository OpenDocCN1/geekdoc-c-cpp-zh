In both cases, we chose the trickier, but often more compact, binary representation. When we move from character-oriented I/O to binary I/O, we give up our usual `>>` and `<<` operators. Those operators specifically turn values into character sequences using the default conventions (e.g., the string `"asdf"` turns into the characters **a**, **s**, **d**, **f** and the integer **123** turns into the characters **1**, **2**, **3**). If we wanted that, we wouldn’t need to say `binary` – the default would suffice. We use `binary` only if we (or someone else) thought that we somehow could do better than the default. We use `binary` to tell the stream not to try anything clever with the bytes.

What “cleverness” might we do to an `int`? The obvious is to store a 4-byte `int` in 4 bytes; that is, we can look at the representation of the `int` in memory (a sequence of 4 bytes) and transfer those bytes to the file. Later, we can read those bytes back the same way and reassemble the `int`:

```
```cpp
ifs.read(as_bytes(i),sizeof(int))    // note: reading bytes
ofs.write(as_bytes(vii),sizeof(int)) // note: writing bytes
```
```

The `ostream write()` and the `istream read()` both take an address (supplied here by `as_bytes()`) and a number of bytes (characters) which we obtained by using the operator `sizeof.` That address should refer to the first byte of memory holding the value we want to read or write. For example, if we had an `int` with the value **1234**, we would get the 4 bytes (using hexadecimal notation) **00, 00, 04, d2**:

![](bbox=[0.1, 0.52, 0.82, 0.58])

The `as_bytes()` function is needed to get the address of the first byte of an object’s representation. It can – using language facilities yet to be explained (§17.8 and §19.3) – be defined like this:

```
```cpp
template<class T>
char* as_bytes(T& i)                 // treat a T as a sequence of bytes
{
    void* addr = &i;                 // get the address of the first byte
                                     // of memory used to store the object
    return static_cast<char*>(addr);  // treat that memory as bytes
}
```
```

The (unsafe) type conversion using `static_cast` is necessary to get to the “raw bytes” of a variable. The notion of addresses will be explored in some detail in Chapters 17 and 18. Here, we just show how to treat any object in memory as a sequence of bytes for the use of `read()` and `write()`.