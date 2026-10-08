behavior, do not store objects directly in a container. Instead store a pointer (or a smart pointer;
§15.2.1). For example:

Click here to view code image

```
vector<Shape> vs;
vector<Shape> vps;
vector<unique_ptr<Shape>> vps;
```

| Il No, don -t there is no room for a Circle or a Smiley ($5.5) |
| Il better, but see $5.5.3 (don't leak) |
| Il OK |

# # 12.2.2 Range Checking

The standard-library vector does not guarantee range checking. For example:

Click here to view code image

```
void silly(vector<Entry>& book) {
    int i = book[book.size()].number;
    Il ...
}
```

Il book.size() is out of range

That initialization is to place some random value in i rather than giving an error. This is
unirable, and out-of-range errors are common problem. Consequently, I often use a simple
range-checking adaptation of vector:

Click here to view code image

```
template<typename T>
struct Vec {
    vector<T> vec;
    using vector<T>::vector;

    T& operator[](int i) { return vec.at(i); }
    const T& operator[](int i) const { return vec.at(i); }

    auto begin() { return checked_iter<vector<T>>(*this).begin(); }
    auto end() { return checked_iter<vector<T>>(*this).end(); }
};
```

| Il use the constructors from vector (under the name Vec) |
| Il range check |
| Il range check const objects; $5.2.1 |
| Il see $13.1 |

Vec inherits everything from vector except the subscript operations that it redefines to do
range checking. The at() is an operation that throws an exception of type
out_of_range if argument is one of the vector's range ($4.2).
For Vec, an out-of-range access will throw an exception that the user can catch. For example:

Click here to view code image

```
void checked(Vec<Entry>& book) {
    try {
        book[book.size()] = {\Joe", 999999;
        Il ...
    } catch (const out_of_range& e) {
        cerr << "range error";
    }
}
```

Il will throw an exception