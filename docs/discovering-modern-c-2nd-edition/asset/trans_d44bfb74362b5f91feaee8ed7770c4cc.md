

```cpp
unsigned size = 100000;
string       many_a(size, 'a');   // Issues with { }^7
string_view  many_a_view(many_a);

string       still_many_a = many_a.substr(0, size/2);
string_view  still_many_a_view = many_a_view.substr(0,
                                                    size/2);
```

当我们从 many_a 创建子字符串时，在本示例中需要拷贝 50,000 个字符。相比之下，string_view 的子字符串仅引用数据而不拷贝任何内容。也就是说，string_view 的子字符串操作是 O(1)，而 string 则是 O(n)，其中 n 是子字符串的长度。我们也可以直接从原始数据构建轻量级子字符串：

```cpp
string_view first_half(&many_a[0], size/2);
```

7. 这里使用 {} 时，编译器会假设我们正在使用初始化列表进行初始化。

与其使用起始位置，不如获取其地址，并将其连同大小一起传递给构造函数。string_view 相对于 string 的另一个优势是，在 C++20 之前它可以在编译时使用（另见 §5.1.1）。

## 4.4.6 span

C++20 中，地址和长度这一概念通过类模板 span<T, Extent> 得到了推广，其中 T 是单个值的类型，Extent 是它们的数量。Extent 的默认值是 dynamic_extent，表示长度在运行时给出。

## C++11 4.4.7 function

=> c++11/function_example.cpp

<functional> 中的 function 类模板是一种通用函数指针。函数类型规范作为模板参数传递，如下所示：

```cpp
double add(double x, double y)
{   return x + y; }

int main ()
{
    using bin_fun = function<double(double, double)>;

    bin_fun f = &add;
    cout << "f(6, 3) = " << f(6, 3) << endl;
}
```

函数包装器可以持有具有相同返回类型和相同参数类型列表的不同种类的函数实体。⁸ 我们甚至可以构建兼容函数对象的容器：

```cpp
vector <bin_fun> functions;
functions.push_back(&add);
```

当函数作为参数传递时，其地址会被自动获取。正如数组会隐式退化为指针一样，函数也会退化为函数指针。因此，我们可以省略取地址运算符 &：

```cpp
functions.push_back(add);
```

当函数被声明为 inline 时，其代码应在调用上下文中插入。当对所有调用都这样做时，生成的可执行文件中可以省略该符号。但是，如果我们在程序的某处获取了函数的地址，编译器会确保它不会被省略：

```cpp
inline double sub(double x, double y)
{   return x - y; }

functions.push_back(sub);
```

同样，地址会被隐式获取。函数对象也可以被存储：

```cpp
struct mult {
    double operator()(double x, double y) const { return x *
    y;
    }
};
```

```cpp
functions.push_back(mult{});
```

这里我们使用默认构造函数构造了一个匿名对象。类模板不是类型，因此我们无法由此创建对象：

```cpp
template <typename Value>
struct power {
    Value operator() (Value x, Value y) const { return pow(x,
    y); }
};
```

```cpp
functions.push_back(power{}); // Error
```

我们只能从已实例化的模板构造对象：

```cpp
functions.push_back(power <double>{} );
```

8. 因此，它们可以具有不同的签名，因为不要求函数名称相同。相比之下，签名相等并不强制要求相同的返回类型。

另一方面，我们可以从包含函数模板的类中创建对象：

```cpp
struct greater_t {
    template <typename Value>
    Value operator() (Value x, Value y) const { return x > y;
    }
} greater_than ;
```

```cpp
functions.push_back(greater_than);
```

在此上下文中，模板调用运算符必须能针对函数类型进行实例化。作为反例，以下语句无法编译，因为我们无法将其实例化为具有不同参数类型的函数：

```cpp
function<double(float, double)> ff = greater_than; // Error
```

成员函数只有在为静态时才能被存储。在以下类中：

```cpp
struct helper
{
    double maxm(double x, double y) const { return x >= y ? x
: y; }
    static double max(double x, double y) { return x >= y ? x
: y; }
};
```

我们有非静态方法 maxm 和静态方法 max。前者只能与对象一起使用，其地址是成员函数指针，类似于该类对象的偏移量。相比之下，方法 max 可以像普通函数一样使用，并可以在此处使用：

```cpp
functions.push_back(helper::max);
```

最后，返回类型和参数类型匹配的 lambda 可以作为函数对象存储：

```cpp
functions.push_back([](double x, double y) { return x / y; });
```

容器中的每个条目都可以像函数一样被调用：

```cpp
for (auto& f : functions)
    cout << "f(6, 3) = " << f(6, 3) << endl;
```

产生预期的输出：

```cpp
f(6, 3) = 9
f(6, 3) = 3
f(6, 3) = 18
f(6, 3) = 216
f(6, 3) = 1
f(6, 3) = 6
f(6, 3) = 2
```

不用说，就灵活性和清晰度而言，这个函数包装器优于函数指针（我们为此付出了一些开销的代价）。

=> c++11/ref_example.cpp

假设我们想要创建一个向量或矩阵列表——可能是很大的列表。此外，假设某些条目出现多次。因此，我们不想存储实际的向量或矩阵。我们可以创建一个指针容器，但我们想避免与之相关的所有危险（§1.8.2）。不幸的是，我们无法创建引用容器：

```cpp
vector<vector<int>&> vv; // Error
```

C++11 为此目的提供了一种名为 `reference_wrapper` 的类引用类型，可以通过头文件 `<functional>` 包含：

此容器可以持有向量的引用：

```cpp
vector<int> v1= {2, 3, 4}, v2= {5, 6}, v3= {7, 8};
vv.push_back(v1);
vv.push_back(v2);
vv.push_back(v3);
vv.push_back(v2);
vv.push_back(v1);
```

它们会被隐式转换为引用包装器（`reference_wrapper<T>` 是针对适用类型的引用的非显式构造函数）。

该类包含一个名为 `get` 的方法，它返回对实际对象的引用，因此我们可以，例如，打印我们的向量：

```cpp
for (const auto& vr : vv) {
    copy(begin(vr.get()), end(vr.get()), ostream_iterator<int>(cout, ", "));
    cout << endl;
}
```

在此处，`vr` 的类型是 `const reference_wrapper<vector<int> >&`。包装器还提供向底层引用类型 `T&` 的隐式转换，可以方便地使用：

```cpp
for (const vector<int>& vr : vv) {
    copy(begin(vr), end(vr), ostream_iterator<int>(cout, "",
    ""));
    cout << endl;
}
```

包装器由两个辅助函数补充：`ref` 和 `cref`，它们位于同一个头文件中。`ref` 对于类型 T 的左值，生成一个引用前者的 `reference_wrapper<T>` 类型对象。如果 `ref` 的参数已经是 `reference_wrapper<T>`，则它只是被拷贝。同样，`cref` 生成一个类型为 `reference_wrapper<const T>` 的对象。这些函数在标准库的多个地方被使用。我们可以使用它们来创建引用的 `std::map`：

```cpp
map<int, reference_wrapper< vector<int> >> mv;
```

鉴于包装器类型名称的长度，使用类型推断来声明它更简短：

```cpp
map<int, decltype(ref(v1)) > mv;
```

映射的常用括号表示法：

```cpp
mv[4]= ref(v1); // Error
```

无法应用，因为包装器没有默认构造函数，而在赋值发生之前，表达式 mv[4] 内部会调用该构造函数。与其使用括号表示法，不如使用 insert 或 emplace：

```cpp
mv.emplace(4, ref(v1));
mv.emplace(7, ref(v2));
mv.insert(make_pair(8, ref(v3)));
mv.insert(make_pair(9, ref(v2)));
```

要遍历条目，再次应用类型推断会更容易：

```cpp
for (const auto& vr : mv) {
    cout << vr.first << ": ";
    for (int i : vr.second.get())
        cout << i << ", ";
}
```

