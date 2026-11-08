
这里，循环的终止条件 `idx < d.size()` 已经检查了循环体中的访问是否被允许。使用 `d.at(idx)` 将是多此一举。

对于 `const` vector，`at` 和 `[]` 自然都会返回 `const Elem&`。

```cpp
// https://godbolt.org/z/GJx51caT
#include <vector>
#include <iostream>
void printAndMore(const std::vector<int>& data) { // by-const-ref
    std::cout << data[0] << std::endl;
    data[0] = 666;        // ✗ doesn't work because 'const int&'
}
int main() {
    std::vector numbers {1,2,3};
    printAndMore(numbers);
}
```

**清单 24.23** 常量容器返回常量引用。

与关联容器不同，当你删除或插入元素时，元素的位置会发生变化。

```cpp
// https://godbolt.org/z/s9PIY6jhv
vector<string> cars{"Diesel", "Petrol", "Super", "Gas"};
cout << cars[1] << '\n';          // Output: Petrol
cars.insert(cars.begin(), "Electricity"); // shifts everything back by one
cout << cars[1] << '\n';           // Output: Diesel
```

**清单 24.24** 这里的“insert”会将所有元素向后移动一位。

通过在 vector 的开头使用 insert，所有数据都会向后移动一个位置，并且 `cars[1]` 的内容会发生变化。在 vector 的任意位置进行 insert 都相对耗时，复杂度为 O(n)，因此应尽量少用。优先使用 `push_back` 和 `emplace_back`。

`vector` 和 `array` 是仅有的具有 `data()` 方法的容器，该方法返回指向第一个元素的*原始指针*。并且由于这两者保证所含元素是*连续存储*的，你可以使用该指针访问所有元素，就像它是一个 C 数组一样。因此，`data()` 非常适合将数据传递给 C 函数，正如你在 **清单 24.25** 中 fread 和 fwrite 的示例所见。在 C++20 中，最好使用 `span` 将指针和长度放在一起，如 **清单 24.26** 所示。

```cpp
// https://godbolt.org/z/Kx1KcP65T
#include <vector>
#include <iostream>
#include <cstdio> // fopen, fclose, fwrite, fread, remove
using namespace std;
ostream& operator<<(ostream& os, const vector<int>&data) {
    for(auto &e : data) os << e << ' '; return os;
}
static const char* FILENAME = "nums.dat";
int main() {
    const vector nums{10,11,22,34};
    {// write
        auto out = fopen(FILENAME, "wb"); // Open file with C for writing
        if(out==nullptr) {
            cerr << "Error opening file\n"; return -1;
        }
        auto ok = fwrite(nums.data(), sizeof(int), nums.size(), out);
        if(ok!=nums.size()) {
            cerr << "Error writing to file\n"; return -1;
        }
        fclose(out); // In C, you must explicitly close. Honestly.
    }
    vector<int> read{};
    {// read
        auto in = fopen(FILENAME, "rb"); // Open file with C for reading
        if(in==nullptr) {
            cerr << "Error opening file\n"; return -1;
        }
        const size_t sz = 4; // assumed, we know we are reading 4 elements ...
        read.resize(sz); // make space for data to be read
        auto ok = fread(read.data(), sizeof(int), sz, in);
        if(ok!=sz) {
            cerr << "Error reading\n"; return -1;
        }
        fclose(in);
    }
    {// Compare
        cout << nums << '\n';    // 10 11 22 34
        cout << read << '\n';    // 10 11 22 34
    }
    if(remove(FILENAME) == -1) {
        cerr << "Warning: Error deleting\n";
    }
}
```

**清单 24.25** 将 `data()` 用作与 C 的接口。

```cpp
#include <iostream>
using namespace std;
int sum(span<const int> area) { // C++20: span
    int sum = 0;
    for(auto e : area) {        // algorithm would be better ...
        sum += e;
    }
    return sum;
}
int main() {
    vector data {1,2,3,4,5};
    cout << sum(data) << "\n";   // implicit container to span
    auto [b, e, sz] = make_tuple(begin(data), end(data), size(data));
    cout << sum(span{b, sz-1}) << "\n"; // 1..4 (Iter, size)
    cout << sum(span{b+1, sz-1}) << "\n"; // 2..5 (Iter, size)
    cout << sum(span{b, e-2}) << "\n"; // 1..3 (Iter, Iter)
    cout << sum(span{b+1, e-1}) << "\n"; // 2..4 (Iter, Iter)
    cout << sum(span{b+2, e}) << "\n"; // 3..5 (Iter, Iter)
    return 0;
}
```

**清单 24.26** 如何使用 `span`。

这里你会看到创建 `span` 的几种方式：

- 从容器隐式创建，例如将其作为参数传递时
- 从迭代器和大小显式创建
- 从两个迭代器显式创建

注意，`std::span<int>` 类型的 area 参数不是按引用传递，而是按值传递，因为它只是一个小对象。

创建 `span` 的其他方式包括从 C 数组、从范围以及当然从另一个 `span` 创建。但反过来也很有用：假设你有一个 C++ 对象，想把它传递给 C API。在前面使用 fwrite 的 **清单 24.25** 中，它本可以像这样：

```cpp
auto write(span<const int> what, FILE* where) { // C++20: span
    return fwrite(what.data(), sizeof(int), what.size(), where);
}
```

`span` 有一个可选的模板参数 `Extent`，用于指定 `span` 在编译时的大小。如果省略它，`span` 就是动态的，如 **清单 24.26** 所示。你不能直接更改 extent 的大小，只能相对于底层容器来更改：

```cpp
span sp{vec.data(), 3};             // the first three elements
sp = span{vec.end()-5, vec.end()};   // Assignment, now the last five elements
```

你可以创建固定大小的 extent，例如，如下一个清单所示。

```cpp
// https://godbolt.org/z/a3qqr1YPM
int car[5]  {1,2,3,4,5};
span span_1 = car;             // directly from a C-array
array arr  {1,2,3,4,5};
span span_2(arr);              // directly from a std::array
vector vec {1,2,3,4,5};
span<int,3> span_3 {vec.data(), 3}; // with 'Extent' from a std::vector
```

**清单 24.27** 这些是固定大小的 span。

当你希望利用编译器在编译时为你执行某些大小检查时，可以使用固定大小的 span：

```cpp
std::array arr{1, 2, 3, 4, 5, 6};  // size 6
std::span<int, 3> sp3{arr.data(), 3}; // Size 3
sp3 = arr;                           // ❌ does not compile
```

`as_bytes(span)` 和 `as_writable_bytes(span)` 这两个自由函数也非常令人兴奋。借助它们，你可以将 `span` 转换为 `span<const byte>` 或 `span<byte>`。你也可以在这里将它们用于 `fwrite()`，甚至更改底层内存位置。

下一个清单展示了如何通过 `span` 写回底层容器的示例。

```cpp
// https://godbolt.org/z/6Ze5GdozG
#include <vector>
#include <span>
#include <iostream>
using namespace std;
void inc(span<int> span) {
    for(auto& e : span) {  // Reference
        e += 1;             // write
    }
}
int main() {
    vector data {1,2,3,4,5};
    span whole{data};                 // 1,2,3,4,5
    inc(whole.first(3));              // -> 2,3,4,4,5
    inc(whole.last(3));               // -> 2,3,5,5,6
    inc(whole.last(4).first(3));      // -> 2,4,6,6,6
    inc(whole.subspan(1,3));           // -> 2,5,7,7,6
    for(auto i: whole) cout << i << ' '; cout << '\n'; // Output: 25776
    return 0;
}
```

**清单 24.28** 你也可以通过“span”进行写入。

这里，`inc()` 通过 `span` 写入容器。此外，你还会看到使用 `first`、`last` 和 `subspan` 创建 `span` 的其他方式。

`span` 还提供 `begin()` 和 `end()` 容器方法，以及 `front()` 和 `back()`，还有 `operator[]`。

### “span”的危险用法

与所有引用一样，你必须小心，确保在使用 `span` 时底层数据不会被销毁。处理临时值时要特别小心：

```cpp
vector<int> create_data() { return {1,2,3,4,5}; }
span<int,5> sp{create_data()};      // ❌ sp references a temporary object
sp = create_data();                  // ❌ this also references a temp-value
for (auto e: span{create_data()}.last(3)); // ❌ references a temp-value
auto data = create_data();           // okay, data is not a temp-value
span ref_data{data};
data.push_back(6);                   // may trigger a reallocation
cout << ref_data[0] << '\n';         // ❌ possibly invalid access
```

C++23 中新增的 `mdspan`（多维 span）工作方式不同。你可以将其叠加到一维数据范围上，`mdspan` 会为你计算索引，以便你可以像使用多维数组一样使用它们。结合 C++23 中新增的另一项特性——`operator[]` 现在可以接收多维索引——它看起来如下一个清单所示。

```cpp
// https://godbolt.org/z/n8jn7v5vb
#include <mdspan>
#include <iostream>
#include <vector>
using namespace std;
int main() {
    //ID: 12 elements
    vector v{1,2,3,4,5,6,7,8,9,10,11,12};
    //2D: as 2 rows with 6 ints each
    auto ms2 = mdspan(v.data(), 2, 6);
    //3D: as a cuboid with 2 layers, 3 rows, 2 columns
    auto ms3 = mdspan(v.data(), 2, 3, 2);
```
