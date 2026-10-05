# 22.5 Reading Data

The following listing presents two simple helper
functions handle reading and writing.

```
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
    return data; // not copied (RVO)
}

void pack(const string fName, const string& fName) {
    auto data = readfile(fName); // read input
    GZWriteStream gz(fName); // initialize output
    gz << data;
}
```

**Listing 22.3** This part of "gzpack.cpp" handles reading and writing the
files.

It is somewhat tricky to read the data in one go into a
vector<char>. First, tell() determines the position of the
end of the file, which was previously jumped to with
seek(). Another seek() brings the read position back to the
beginning so that file.read() reads from the start of
the file. There could have been other ways to determine
the file size, but they are not necessarily less
complicated than this.

The vector<char>::data() function returns a char*, into
which ifstream::read() reads the data directly into the
g