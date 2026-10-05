```
auto out = fopen(FILENAME, "wb"); // Open file C for writing
if(out==nullptr) {
    cerr << "Error opening file\n"; return -1;
}
auto ok = fwrite(nums.data(), sizeof(int), nums.size(), out);
if(ok!=nums.size()) {
    cerr << "Error writing to file\n"; return -1;
}
fclose(out); // In C, you must explicitly close. Honestly.

vector<int> read() {
    // read
    auto in = fopen(FILENAME, "rb"); // Open file C for reading
    if(in==nullptr) {
        cerr << "Error opening file\n"; return -1;
    }
    const size_t sz = 4; // assumed, we now read 4 elements
    read.resize(sz); // make space for data to be read
    auto ok = fread(read.data(), sizeof(int), sz, in);
    if(ok!=sz) {
        cerr << "Error reading\n"; return -1;
    }
    fclose(in);
    return read;
}

// Compare
cout << nums << "\n";
cout << read() << "\n"
10 11 22 34
10 11 22 34
if(remove(FILENAME) == -1) {
    cerr << "Warning: Error deleting\n";
}
```

# Listing 24.25 Use data() as an interface to C.

In Listing 24.25, I use the functions read and fwrite from the <stdio> header of the C standard library. Each these take a void* for the data as the first parameter and then two additional parameters to calculate the size of the data to be read: first the size of each individual element, here sizeof(int), and second the number of int. When reading, it makes easy for myself here and assume I want to read int values. In real life, you would probably find out how many elements you want to read.

Note that the data() pointer (is also the case for iterators) is only valid until you add an element to the vector and thereby change its capacity.

# Access via Spans

An extension—that is, span—serves as access to a vector (or an array). The previous section provided an overview of this. The span class since C++20 is so useful that I would like to go into more detail about it in this separate section.

A typical use case is that you want to pass a container to a parameter to a function. Without span, it would look like this:

```
// very specific parameter type
```