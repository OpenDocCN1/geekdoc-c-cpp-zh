

如果T支持算术、按位和/或布尔运算（通常如此），那么valarray最有用——支持得越多越好。如果T支持三角函数等运算（如double那样），那就更完美了。

| 容器 | 描述 |
|---|---|
| `valarray<T>` | 与其他容器不兼容；用于在一个或多个维度上快速处理数值数据 |
| `slice` | valarray的选定范围 |
| `gslice` | valarray的选定范围 |
| `slice_array` | 用于选择valarray范围的辅助类 |
| `gslice_array` | 用于选择valarray范围的辅助类 |
| `mask_array` | 用于掩码valarray部分的辅助类 |
| `indirect_array` | 用于valarray重排视图的辅助类 |

**表24.14** 简介：非标准“valarray”容器。

使用自定义数据类型并没有什么问题，只是优化可能不适用。你完全有可能在特定硬件上与第三方库一起使用或必须使用特殊数据类型。例如，较旧的GPU在其CUDA库中仅支持float而不支持double，但此后它们已经进步了。CUDA现在是广泛使用的显卡接口——比valarray的使用更为普遍。当速度比精度更重要时，半精度浮点数（16位浮点数）可能很有用。自C++23起，有一个可选的內置数据类型float16_t（参见第4章，第4.4.4节）。或者你可以使用其他库。你会找到类似float16、half、HalfFloat或__fp16等名称。CUDA现在支持它，并用于例如表面纹理。CUDA和valarray有点矛盾；你的应用程序中可能会有重叠。

> **不要将指针放入“valarray”**
> 
> `valarray`代表*值数组*，因此它用于值，而不用于任何形式的间接引用。即使实现并不阻止这种使用，你也应该避免这样做。对于这种目的，请使用vector。

将本节中的示例嵌入以下模板中（并注意我在清单24.12后面的框中对<<=的评论）：

```cpp
// https://godbolt.org/z/r11584wEf
#include <valarray>
#include <iostream>
using namespace std;

template<typename T>
ostream& operator<<(ostream &os, const valarray<T>& a) { // <<'s with newline
    for(const auto &v : a) os << v << ' ';
    return os << '\n';
}
int main() {
    // ... example code here ...
}
```

### 24.12.2 初始化

尽管valarray并不像vector那样真正可调整大小，你仍然可以通过完全复制来调整valarray的大小。因此，你可以不带参数或使用预定义大小来初始化valarray：

```cpp
// https://godbolt.org/z/chnj64dva
valarray<int> data;                 // initially size 0
cout << data.size() << "\n";        // Output: 0
data.resize(100);                    // enlarged
cout << data.size() << "\n";        // Output: 100
valarray<int> data2(200);            // space for 200 values
cout << data2.size() << "\n";       // Output: 200
valarray<int> dataC(5, 20);          // twenty 5s, different from vector
cout << dataC.size() << ", dataC[6]=" << dataC[6] << "\n"; // Output: 20, dataC[6]=5
valarray<int> dataD{ 2, 3, 5, 7, 11 }; // syntactically initialization list
cout << dataD.size() << ", dataD[3]=" << dataD[3] << "\n"; // Output: 5, dataD[3]=7
```

如你所见，你还可以用初始值预定义一系列值。但请注意：valarray(value, size) 的两个参数与vector的顺序相反！最好习惯只用大小数值或初始化列表来定义valarray。

也允许复制和移动。

slice_array、gslice_array、mask_array和indirect_array辅助类中的每一个也可以指定为初始化的来源。请注意，这些构造函数未标记为explicit，允许参数和返回值的隐式转换。

### 24.12.3 赋值

赋值运算符operator=支持与构造函数相同的参数。

没有像许多其他（真正的）容器那样的assign，但至少有一个swap。

### 24.12.4 插入和删除

你不能像使用insert那样真正地插入。不过，你可以通过`operator[]`对元素进行读写访问。访问不进行边界检查；你必须自己注意范围边界。没有用于此目的的`at()`方法。

但是，你仍然可以在之后更改valarray的大小。为此，有`resize`方法：

- `resize(size_t size)`—扩大或缩小，截断或使用`{}`初始化
- `resize(size_t size, T value)`—扩大或缩小，截断或使用value初始化

此操作期间可能会复制所有数据。因此，指向valarray的指针和迭代器将失效。

### 24.12.5 访问

`operator[]`在valarray中几乎可以说是神奇的。它不仅可以处理整数索引来寻址单个元素，还可以使用切片、掩码和间接引用作为索引。

事实上，前述辅助类被用作索引，但在实践中，这里会发生许多类型转换，因此你使用以下类型作为索引：

- **切片**  
  你可以使用`slice`或`gslice`。
- **掩码**  
  使用与数据`valarray<T>`大小相同的`valarray<bool>`。
- **间接引用**  
  使用与数据`valarray<T>`大小相同的`valarray<size_t>`。

考虑以下示例：

```cpp
// https://godbolt.org/z/PeG4K7Edc
valarray v { 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12 };
valarray<int> r1(v[slice(0, 4, 3)]); // Start at 0, 4 elements, step size 3
cout << r1;                          // Output: 1 4 7 10
valarray<int> r2(v[v > 6]);          // addressed by valarray<bool>
cout << r2;                          // Output: 7 8 9 10 11 12
const valarray<size_t> indirect{ 2, 2, 3, 6 }; // duplicates allowed
valarray<int> r5(v[indirect]);       // addressed by valarray<size_t>
cout << r5;                          // Output: 3 3 4 7
```

### 24.12.6 特色：操作所有数据

有少数几个有用的方法用于获取valarray中所有数据的信息或对它们进行操作：

- **sum、min 和 max**  
  计算所有值的总和、最小值和最大值。对于普通容器，你可能会使用`<algorithm>`中的`accumulate`或`max_element`等。
- **shift 和 cshift**  
  在整个`valarray`上移动和旋转值。`shift`进行旋转；`cshift`用零填充。
- **apply**  
  对`valarray`中的每个元素调用一个函数。该函数必须接受一个`T`作为参数并返回`T`。你不能修改元素。总体而言，你会从`apply`得到一个新的`valarray`。对于普通容器，你可能会使用`for_each`。
- **整数、浮点、布尔和按位运算**  
  你可以使用所有内建运算符同时修改`valarray`的所有值：`+`、`*`、`+=`、`!`、`&&`、`<<`等。你可以指定一个单一值（标量）或者，如果合适，另一个`valarray`作为另一个操作数。写出`va * vb`等同于`va[0]*vb[0]; va[1]*vb[1]; ...`这适用于所有二元运算符。
- **数学函数**  
  对于`valarray`，重载了大量数学函数，它们会逐元素地应用于所有包含的值。示例包括`abs`、`exp`、`sqrt`、`log10`、`sin`、`cos`、`asin`和`cosh`。每次你都会收到一个新的`valarray`，就像调用了`apply(func)`一样。
- **比较运算**  
  你可以使用`operator>`等将`valarray`的所有元素与单个值或另一个`valarray`进行比较。你会得到一个`valarray<bool>`。

### 24.12.7 特色：切片和掩码

与普通容器相比，其特殊之处在于你可以使用辅助类对`valarray`进行切片，只选择其中的一部分。这些切片可能很复杂，例如包含步长，从而模拟多维性。通过掩码，你可以将`valarray`的某些部分排除在操作之外。

切片辅助对象表示对`valarray`的复杂索引，类似于普通数组中a[12]中的12。你可以使用以下构造函数之一创建切片辅助对象：

- `slice()`—空切片
- `slice(size_t start, size_t size, size_t stride)`—用于指定起始位置、大小和步长的参数
- `slice(const slice& other)`—用于副本

