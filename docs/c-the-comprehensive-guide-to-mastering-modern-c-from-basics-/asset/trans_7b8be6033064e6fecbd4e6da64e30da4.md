

# vector<int>::size_type

因此，让编译器来决定正确的类型。然而，你不需要使用 `?`，而是使用 `auto` 关键字。

```
// https://godbolt.org/z/wh71cf7j1
#include <vector>
#include <set>
#include <iostream> // cout
using std::vector; using std::set; using std::cout;
using vector_t = vector<unsigned long>; // 你自己的类型别名
int main() {
    vector_t huge{12ULL, 100000000000ULL, 9ULL, 0ULL };
    auto sz = huge.size();
    auto uisui = huge.size();
    for(auto it = huge.begin(); it != huge.end(); ++it) {
        *it = 2; // double
    }
    set sorted(huge.begin(), huge.end()); // set<vector_t::value_type>
    for(auto val : sorted) {
        cout << val << " ";
    }
    cout << "\n";
}
```

在初始化变量时，编译器可以确定类型。

如你所见，剩余的类型指定并不多。在任何使用表达式初始化变量的地方都可以使用 `auto`。编译器知道初始化表达式的类型，并将其设置为变量的类型。

> “auto” 永久设置了写入变量的类型

需要注意的是，`auto` 等同于手动编写类型。该类型被真正固定了，无法更改。

- 列表 12.33

事实并非如人们预期的那样——即你创建一个可变类型的变量。该变量的所有使用都是这种类型。无法用新类型进行重新赋值：

```
auto value = 12; // value 现在是一个 int
value = string("Hello"); // 不可能的不同类型的重新赋值
```

然而，`auto` 声明变量允许较大的自由，并且告诉代码读者的信息比显式类型要少。因此，从 C++20 开始，你可以用变量必须满足的 concept（概念）来限制 `auto`。在这种情况下，之前的示例可以像下面的列表一样：

```
// https://godbolt.org/gZWchWoeK
#include <vector>
#include <set>
#include <iostream> // cout
#include <concepts> // integral
#include <iterator> // output_iterator, input_iterator
namespace std;
using vector_t = vector<unsigned long long>; // 你自己的类型别名
int main() {
vector_t huge{12ULL, 1000000000ULL, 9ULL, 0ULL},
unsigned_integral auto sz = huge.size();
unsigned_integral auto uiui = huge[sz];
signed integral me = huge[1]; // 未满足 concept
input_output_iterator auto itx = huge.begin(); // 没有参数的 concept
for(output_iterator unsigned long long auto it = huge.begin();
it!=huge.end(); ++it)
    *it = 2; // double it
/* 使用 set 排序 */
set sorted(huge.begin(), huge.end()); //
set<vector_t::value_type>
for(const unsigned_integral auto& val : sorted)
    cout << val << val << " ";
}
cout << "\n";
}
```

## 列表 12.34 使用 “auto” 的类型推导可以使用 concept 进一步限制。

你可以用 `const` 和 `&` 等修饰符来丰富 `auto` 以调整最终类型。引用在这里有时特别至关重要。这样你得到的不是拷贝，而是一个你可以修改的引用。

```
// https://godbolt.org/z/ro6fdsvT9
#include <vector>
#include <iostream> // cout

using std::vector; using std::cout;
int main() {
	vector<int> data = {12, 100, -1, 0}; // vector<int>
	for(auto& val : data) {
		val *= 2; // double it
	}
	for(const auto val : data) {
		cout << val << " ";
	}
    cout << "\n";
}
```

## 列表 12.35 当你用 & 丰富 "auto" 时，你将得到一个可修改的引用。

第一个 `auto` 必须用 `&` 丰富，这样你才能获得想要通过 `val *= 2` 修改的实际数据的引用。如果你只写了 `for(auto : data)`——不带 `&`——那么 `val` 每次都是一个拷贝，`val *= 2;` 对 `data` 的内容将没有任何影响。

对于第二个 `auto`，完全没问题，因为你不需要为了输出修改 `val`。而且为了确保这种情况不会意外发生，你可以通过丰富 `const` 来保护自己免受意外更改的影响。因此，每个元素被拷贝到 `val`，标记为常量并输出。

对于 `int`，这种拷贝是没问题的。但是，如果元素巨大且拷贝开销很大，你应该结合这两种修饰。假设 `Image` 是一个拷贝昂贵的类，建议结合 `const` 和 `auto` 使用使用：

```
vector<Image> data{Image("MonaLisa.png"), "Scream.png"};
for(const auto& image : data)
    show(image);
```

回到原始示例，还有几行无法使用 `auto`：

```
vector_t huge{12ULL, 100000000000ULL, 9ULL, 0ULL};
// ...
set sorted(huge.begin(), huge.end());
```

对于 `huge`，编译器无法使用 `auto`，因为你需要知道 `set<unsigned long long>`。当你使用 `initializer_list` 初始化 `auto` 时，编译器已经知道：

```cpp
set<vector_t::value_type> sorted(huge.begin(), huge.end());
```

## 12.13 标准容器中的自定义类

