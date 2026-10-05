
declarations also apply only within the namespace and do not affect the outside.

Next, I define the class that bundles the main functionality of the C library. In this example, all three relevant C functions are already included. Based on the names, you can probably guess the meanings and some of the operating rules:

- Gzopen() opens a file. If it fails, the function returns a special value according to C conventions.
- Gzclose() closes a correctly opened file. The call is not necessary if gz-open failed.
- Gzwrite() writes data to the output. A return value greater than zero indicates success.

```cpp
// https://godbolt.org/z/Yh7j1WEGc
// RAII wrapper
class GzWriteStream {
public:
    GzFile gz_; // C struct from zlib.h
    explicit GzWriteStream(const string& filename)
        : gz_(gzopen(filename.c_str(), "wb")) // 'w': write, 'b': binary,
{
        if(gz_==NULL) throw runtime_error(std::strerror(errno));
    }
    ~GzWriteStream() {
        fclose(gz_);
    }
    GzWriteStream& operator<<=(const span<char> &data) {
        write(data);
        return *this;
    }
private:
    void write(span<char> data) { // C++20
        auto bytes = std::as_bytes(data);
        auto res = gzwrite(gz_, bytes.data(), size(bytes));
        if(res==0) throw std::runtime_error("Error writing");
    }
    GzWriteStream(const GzWriteStream&) = delete; // no copy
    GzWriteStream& operator=(const GzWriteStream&) = delete; // no assignment
};
```

**Listing 22.2** This part of "gzpack.cpp" contains all the C functions used.

As a data field, GzWriteStream contains the gz_ handle as a connection to zlib and thus to the opened file. In the constructor's init list, gzopen() opens the file and assigns the result to the handle. The documentation states that a return value of NULL indicates an error. Then the global errno variable shows the exact error. You can decode this code with strerror. More importantly, you should also throw an exception and exit the code this way, instead of jumping out and running to the end.

If gzopen() fails, then gzclose() is not necessary. Therefore, this is an optimal use case for using the destructor. If an exception leaves the constructor instead of running normally, the GzWriteStream object is considered not created. Thus, no destructor is called—either.

The first parameter gzopen() receives the file name as a C string. From the filename parameter of string, you can obtain the file name as a C string using the c_str() method. The second parameter "wb9" indicates that the file is opened for writing ('w' for write). The 'b' stands for binary format. The alternative 't' for text format would potentially convert individual characters. The final '9' stands for maximum data compression.

## 22.3 C Resources

Packing the gzopen() and gzclose() function pair together in the constructor and destructor of a class is particularly suitable here, as these two always need to be called in pairs. There is no (successful) gzopen() without gzclose(), and no gzclose() without gzopen().

You deal with such pairings in many C interfaces. Whether it's initializing the entire library or acquiring and releasing a paintbrush for the window frame—such function pairs are common, and such a wrapper class is then appropriate.

In GzWriteStream, I have included even more functionality. Sometimes, however, you only need the pairing of two functions. Then it might be tedious to write a separate wrapper class for each pair. If that is too much work for you, you can fall back on your acquaintance shared_ptr: you can use it in the variant where the constructor takes not one but two arguments.

The second argument here is a function object, which is called within the destructor of shared_ptr. shared_ptr calls this a custom deleter.

I will make a brief digression here, because as a function object you see a lambda—a function without a name—and within it gzclose() is called:

```cpp
std::shared_ptr<gzFile_s> gz(
  gzopen(fNameOut.c_str(), "wb9"),
  [](gzFile_s* f) { gzclose(f); }
);
if(gz.get() == NULL) throw std::runtime_error("Error");
```

You will learn more about this in Chapter 23, Section 23.3.

You can almost always use this pattern with the shared_ptr constructor with two arguments for simple pairings of C functions.

## 22.4 “void” Pointers

The third function, gzwrite(), takes two parameters: a void* to the data and the length of the data. The return value is the amount of data written; a value of zero indicates an error.

But what exactly is void*? Did you notice that our own write() function, using the as_bytes function, created a span<byte> method data() returns a const byte*, which I then passed to the void* of gzwrite()? Normally, C++ always complains when you take a variable of one type and try to use it as something else. Imagine if gzwrite() took an int: then the const byte... (Wait, the text seems fragmented/garbled here). *Self-correction based on OCR flow*: 

The text in page 962-963 seems to have some OCR-garbled repetitions or ghost text. I will reconstruct the logical flow:

The third function, gzwrite(), takes two parameters: a void* to the data and the length of the data. The return value is the amount of data written; a value of zero indicates an error.

But what exactly is void*? Did you notice that our own write() function, using the as_bytes function, created a span<byte> method data() returns a const byte*, which I then passed to the void* of gzwrite()? Normally, C++ always complains when you take a variable of one type and try to use it as something else. Imagine if gzwrite() took an int: then the const byte... [Note: The OCR text in 962-963 is highly repetitive/corrupted, I will output the clear sentences provided].

## 22.5 Reading Data

The following listing presents two helper functions.

```cpp
// https://godbolt.org/z84TcbWjj
std::vector<char> readfile(const string& fName) {
    std::ifstream file(fName, std::ifstream::binary);
    if(!file) throw std::runtime_error("Error opening input");
    file.seekg(0, file::end()); // jump to the end of the file
    const auto length = file.tell(); // current position is file size
    if(length > 1024*1024*1024)
        throw std::runtime_error("No more than 1 GB please");
    file.seekg(0, file::beg); // back to the beginning
    std::vector<char> data(length); // allocate space
    file.read(data.data(), length); // read in one go
    return data; // not copied (RVO))

void pack(const string fName, const string& fName) {
    auto data = readfile(fName); // read input
    GZWriteStream gz(fName); // initialize output
    gz << data;
}
```

**Listing 22.3** This part of "gzpack.cpp" handles reading and writing the files.

It is somewhat tricky to read the data in one go into a vector<char>. First, tell() determines the position of the end of the file, which was previously jumped to with seek(). Another seek() brings the read position back to the beginning so that file.read() reads from the start of the file. There could have been other ways to determine the file size, but they are not necessarily less complicated than this.

The vector<char>::data() function returns a char*, into which ifstream::read() reads the data directly into the g.
