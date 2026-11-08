+   - `Gzopen()` opens a file. If it fails, the function returns a special value according to C conventions.
+   - `Gzclose()` closes a correctly opened file. The call is not necessary if `gz-open` failed.
+   - `Gzwrite()` writes data to the output. A return value greater than zero indicates success.

```
```cpp
// https://godbolt.org/z/Yh7j1WEGc
class GzWriteStream {                         // RAII wrapper
public:
    gzFile gz_;                                // C struct from zlib.h
    explicit GzWriteStream(const string& filename)
        : gz_{gzopen(filename.c_str(), "wb9")} // 'w': write, 'b':binary, '9':level
    {
        if(gz_==NULL) throw std::runtime_error(std::strerror(errno));
    }
    ~GzWriteStream() {
        gzclose(gz_);
    }
    GzWriteStream& operator<<(const span<char>& data) {
        write(data);
        return *this;
    }
private:
    void write(span<char> data) {
        auto bytes = std::as_bytes(data);             // C++20
        auto res = gzwrite(gz_, bytes.data(), size(bytes));
        if(res==0) throw std::runtime_error("Error writing");
    }
    GzWriteStream(const GzWriteStream&) = delete;    // no copy
    GzWriteStream& operator=(const GzWriteStream&) = delete; // no assignment
};
```
```

**Listing 22.2** This part of "gzpack.cpp" contains all the C functions used.

As a data field, GzWriteStream contains the gz_ handle as a connection to zlib and thus to the opened file. In the constructor's init list, gzopen() opens the file and assigns the result to the handle. The documentation states that a return value of NULL indicates an error. Then the global errno variable shows the exact error. You can decode this code with strerror. More importantly, you should also throw an exception and exit the code this way, instead of jumping out with a return or running to the end.

If gzopen() fails, then gzclose() is not necessary. Therefore, this is an optimal use case for using the destructor. If an exception leaves the constructor instead of running normally, the GzWriteStream object is considered not created. Thus, no destructor is called—and no gzclose() either.