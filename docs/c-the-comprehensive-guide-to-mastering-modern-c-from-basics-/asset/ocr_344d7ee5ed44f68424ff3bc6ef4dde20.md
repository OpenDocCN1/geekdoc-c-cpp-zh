# Write Your Classes Such That You Can Apply the Rule of Zero

If you use the corresponding structures of the standard library instead of the fields with ownership problems, the compiler will generate suitable copy and move operations as well as the destructor for your class.

Then you do not define or declare *any* of the big five operations for your class.

The previous example now becomes almost trivial. Depending on the use case, simply use a vector or smart pointers.

```
// https://godbolt.org/z/nbh9aozPM
#include <vector>
#include <memory> // unique_ptr, shared_ptr
struct Type1 {\ // automatic complete copy of the resource
    std::vector<char> data;
    Type1(int n) : data(n) {}
};
struct Type2 {\ // copy prohibited, move allowed
    std::unique_ptr<int[]> data;
    Type2(int n) : data(new int[n]) {}
};
struct Type3 {\ // copy allowed, resource is then cleanly shared
    std::shared_ptr<Type1> data;
    Type3(int n) : data(std::make_shared<Type1>(n)) {nn};
```

Listing 17.2 Instead of using a raw pointer, use a standard construct and do not define any of the big five operations.

# First: Third-party

# 17.1.4 Exceptions to the Rule of Zero