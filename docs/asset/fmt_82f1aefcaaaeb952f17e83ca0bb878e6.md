
- 影响：如果是空指针，则分配一个未指定大小的 `long` 数组，并将第一个元素存储在 `iarray` 中。然后扩展 `iarray` 指向的数组以包含该元素。新分配的元素初始化为零。在对对象的任何操作后，返回的引用可能无效。然而，如果函数失败且是 `basic_io` 对象的子类，其效果等同于对派生类调用 `setstate(badbit)`（可能会抛出异常）。
- 返回：初始化为0 的 `iarray[idx]`。

```cpp
void* pword(int idx);
```

- 影响：如果是空指针，则分配一个未指定大小的 `void` 指针数组，并将第一个元素存储在 `array` 中。然后扩展 `array` 指向的数组以包含该元素。新分配的元素初始化为零，相同索引的值将产生相同值的引用。如果函数失败且是 `basic_io` 对象的子类，其效果等同于对派生类调用 `setstate(badbit)`（可能会抛出异常）。由于所引的存储引用被保留了，因此在下一次调用 `copyfmt` 之前，相同索引的 `pword` 将返回相同值的引用。
- 返回：成功时返回 `array[idx]`。一个初始化为 0 的有效 `void*`。
- 注意：在同一对象对象的后续调用 `pword(int)` 后，早期的返回值可能不再有效。

# ISO/IEC 14882:2017(E)

## 30.5.3.6 ios_base_callback 回调 [ios.base.callback]

```cpp
void register_callback(event_callback fn, int index);
```

- 1 影响：注册对 `(fn, index)`，在调用 `imbue()` (30.5.3.3)、`copyfmt()` 或 `-ios_base()` (30.5.3.7) 期间，将使用参数 `index` 调用函数 `fn`。已注册的函数在事件发生时被调用，顺序与注册顺序相反。在回调函数激活期间注册的函数将直到下一次事件发生前有效。
- 2 需求：函数 `fn` 不得抛出异常。
- 3 备注：相同的对不会合并。注册两次的函数会被调用两次。

## 30.5.3.7 ios_base 构造函数/析构函数 [ios.base.cons]

```cpp
ios_base();
```

- 1 影响：每个 `ios_base` 成员在构造后具有不确定的值。对象的成员应在首次使用之前或析毁之前通过调用 `basic_init` 初始化，以先发生者为准；否则行为未。

```cpp
-ios_base();
```

- 2 影响：销毁 `ios_base` 类的对象。每个注册的回调对 `(fn, index)` (30.5.3.6) 以 `(*erase_event, *this, index)` 的形式处理，此时从内部调用的任何 `ios_base` 成员函数都具有定义良好的结果。

## 30.5.4 类模板 fpos [fpos]

```cpp
namespace std {
template <class state> class fpos {
public:
// 30.5.4.1, 成员
    state state() const;
    void state(stateT);
private:
    state st; // 仅供说明使用
};
}
```

## 30.5.4.1 fpos 成员 [fpos.members]

```cpp
void state(stateT);
state state() const;
```

- 2 返回：`st` 的当前值。

## 30.5.4.2 fpos 要求 [fpos.operations]

- 1 允许执行表 112 中指定的运算。其中：
    - (1.1) `P` 指向 `fpos` 实例。
    - (1.2) `p` 和 `q` 指向类型 `P` 的值，
    - (1.3) `O` 指向类型 `streamoff` 的值，
    - (1.4) `o` 指向类型 `streamoff` 的值，
    - (1.5) `sz` 指向类型 `streamsize` 的值以及
    - (1.6) `i` 指向类型 `int` 的值。

表 112 — 位置类型要求

| 表达式 | 类型 | 操作语义 | 断言/备注前置/后置条件 |
| --- | --- | --- | --- |
| P(i) | | | p == F(i) 备注：假设有一个析构函数。后置条件：p == F(i)。 |
| P p(i); | | | |
| P = i; | | | |
| P(o) | fpos | 从偏移转换 | O(p) == p |
| 0(p) | streamoff | 转换为偏移 | == 是一个等价关系 |
| p == q | 可转换为 bool | | |
| p != q | 可转换为 bool | !(p == q) | |
| q + o | fpos | + 偏移 | q - o == p |
| p += o | | | | |
| p -= o | | - 偏移 | q + o == p |
| o = p - q | streamoff | 距离 | | |
| streamsize(o) | streamsize | 转换 | streamsize(O(sz)) == sz |
| 0(sz) | streamoff | 转换 | streamsize(O(sz)) == sz |

- 备注：如果实现需要满足 `fpos` 上的重载运算符以满足 30.5.4.2 的要求。不确定这些运算符是 `fpos` 的、全局运算符还是通过其他方式提供的。 — 备注结束
- 返回类型为 `pos_type` 值的运算：返回 `P(-1)` 作为无效值以指示错误。如果此值用作 `istream`、`ostream` 或 `streambuf` 成员接受类型为 `pos_type` 的参数，则该函数的行为是定义的。

## 30.5.5 类模板 basic_ios

### 30.5.5.1 概述 [ios] [ios.overview]

```cpp
namespace std {
template <class char, class traits = char_traits<char>>
class basic_ios : public ios_base {
public:
    using char_type = char;
    using int_type = typename traits::int_type;
    using pos_type = typename traits::pos_type;
    using off_type = typename traits::off_type;
    using traits_type = traits;
    // 30.5.5.4, 标记函数
    explicit operator bool() const;
    bool rstate() const;
    void clear(istream state = goodbit);
    void setstate(istream state);
    bool good() const;
    bool eof() const;
    bool fail() const;
    bool bad() const;
    iostate exceptions() const;
};
}
```

## 30.5.5.2 basic_ios 构造函数

```cpp
explicit basic_ios(basic_streambuf<charT, traits*> sb);
~basic_ios();
```

- 1 影响：构造一个 `basic_ios` 类 (30.5.3.7) 对象。对象的成员应在首次使用之前或析毁之前通过调用 `basic_init` 初始化，以先发生者为准；否则行为未。

## 30.5.5.3 成员函数 [basic_ios]

```cpp
basic_streambuf<charT, traits>* rdbuf() const;
```
- 1 返回：关联缓冲区。

```cpp
basic_streambuf<charT, traits>* rdbuf(basic_streambuf<charT, traits>* new);
```
- 2 影响：设置缓冲区。
- 3 返回：之前的缓冲区。

```cpp
char_type fill() const;
```
- 4 返回：用于填充输出的字符。

```cpp
char_type fill(char_type fillch);
```
- 5 影响：设置填充字符。
- 6 返回：之前的填充字符。

```cpp
int width() const;
```
- 7 返回：当前的宽度。

```cpp
void width(int n);
```
- 8 影响：设置宽度。
- 9 返回：之前的宽度。

```cpp
int precision() const;
```
- 10 返回：当前的精度。

```cpp
void precision(int n);
```
- 11 影响：设置精度。
- 12 返回：之前的精度。

```cpp
const locale& getloc() const;
```
- 13 返回：区域。

```cpp
basic_ios& getloc(const locale& loc);
```
- 14 返回：新的区域。
- 15 返回：之前的区域。

```cpp
iostate exceptions() const;
```
- 16 返回：异常状态。

```cpp
void exceptions(iostate what);
```
- 17 影响：调用 `setstate(what)`。
- 18 返回：之前的异常状态。

```cpp
void setstate(istream state);
```
- 19 影响：设置状态。

```cpp
bool good() const;
```
- 20 返回：如果状态是良好的。

```cpp
bool eof() const;
```
- 21 返回：如果到达流末尾。

```cpp
bool fail() const;
```
- 22 返回：如果逻辑操作失败。

```cpp
bool bad() const;
```
- 23 返回：如果发生了致命错误。

```cpp
int rstate() const;
```
- 24 返回：当前状态。

```cpp
void clear(istream state = goodbit);
```
- 25 影响：清除状态。

# ISO/IEC 14882:2017(E)

```cpp
void swap(basic_ios& rhs) noexcept;
```

影响：`*this` 和 `rhs` 的状态将交换*，但 `rdbuf()` 将返回与调用前相同的值，且 `rdbuf()` 将返回与调用前相同的值。

```cpp
void set_rdbuf(basic_streambuf<char, traits**> sb);
```

```cpp
sb != nullptr;
```

影响：在不调用 `clear()` 的情况下，将此流与 `sb` 指向的 `basic_streambuf` 对象关联。

后置不变条件：`rdbuf() == sb`。

抛出异常：无异常。

# 30.5.5.4 basic_ios 标志函数 [iostate.flags]

```cpp
explicit operator bool() const;
```

返回值：`!fail()`

```cpp
bool operator!() const;
```

返回值：`fail()`

```cpp
iostate rstate() const;
```

返回值：流缓冲区的错误。

```cpp
void clear(iostate state = goodbit);
```

后置不变条件：如果 `rdbuf() != 0`，则调用 `rstate()`；否则 `rstate() == (state | ios_base::badbit)`。

影响：如果 `((state | (rdbuf() ? goodbit : badbit)) & exceptions()) == 0`，否则该函数将抛出一个 `basic_ios::failure` (30.5.3.1.1) 对象，由实现定义的参数值构造。

```cpp
void rstate(iostate state);
```

影响：调用 `clear(rstate() | state)`（这可能会抛出 `basic_ios::failure` (30.5.3.1.1)

```cpp
bool good() const;
```

返回值：`rstate() == 0`

```cpp
bool eof() const;
```

返回值：如果 `rstate()` 中设置了 `eof`，则返回 true。

```cpp
bool fail() const;
```

返回值：如果 `rstate()` 中设置了 `failbit` 或 `badbit`，则返回 true。

```cpp
bool bad() const;
```

返回值：如果 `rstate()` 中设置了 `badbit`，则返回 true。

```cpp
iostate exceptions() const;
```

返回值：一个掩码，用于确定 `rstate()` 中设置哪些元素会导致抛出异常。

> 针对 `fail()` 同样检查 `badbit` 是一种历史做法。

# ISO/IEC 14882:2017(E)

```cpp
void exceptions(iostate except);
```

后置不变条件：`except == exceptions()`

影响：调用 `clear(rdstate())`。

# 30.5.6 ios_base 操纵符

# 30.5.6.1 fstflags 操纵符

```cpp
ios_base boolalpha(ios_base& str);
```

影响：调用 `str.setf(ios_base::boolalpha)`。

返回值：`str`。

```cpp
ios_base noboolalpha(ios_base& str);
```

影响：调用 `str.unsetf(ios_base::boolalpha)`。

返回值：`str`。

```cpp
ios_base showbase(ios_base& str);
```

影响：调用 `str.setf(ios_base::showbase)`。

返回值：`str`。

```cpp
ios_base noshowbase(ios_base& str);
```

影响：调用 `str.unsetf(ios_base::showbase)`。

返回值：`str`。

```cpp
ios_base showpoint(ios_base& str);
```

影响：调用 `str.setf(ios_base::showpoint)`。

返回值：`str`。

```cpp
ios_base noshowpoint(ios_base& str);
```

影响：调用 `str.unsetf(ios_base::showpoint)`。

返回值：`str`。

```cpp
ios_base showpos(ios_base& str);
```

影响：调用 `str.setf(ios_base::showpos)`。

返回值：`str`。

```cpp
ios_base noshowpos(ios_base& str);
```

影响：调用 `str.unsetf(ios_base::showpos)`。

返回值：`str`。

```cpp
ios_base skipips(ios_base& str);
```

影响：调用 `str.setf(ios_base::skipips)`。

返回值：`str`。

```cpp
ios_base noskipips(ios_base& str);
```

影响：调用 `str.unsetf(ios_base::skipips)`。

返回值：`str`。

[std::ios.manip]
[fmtflags.manip]

```cpp
ios_base& uppercase(ios_base& str);
```

影响：调用 `str.setf(ios_base::uppercase)`；

返回值：`str`。

```cpp
ios_base& neouppercase(ios_base& str);
```

影响：调用 `str.unsetf(ios_base::uppercase)`。

返回值：`str`。

```cpp
ios_base& unitbuf(ios_base& str);
```

影响：调用 `str.setf(ios_base::unitbuf)`。

返回值：`str`。

```cpp
ios_base& nounitbuf(ios_base& str);
```

影响：调用 `str.unsetf(ios_base::unitbuf)`。

返回值：`str`。

# 30.5.6.2 adjustfield 操纵符

```cpp
ios_base& internal(ios_base& str);
```

影响：调用 `str.setf(ios_base::internal, ios_base::adjustfield)`。

返回值：`str`。

```cpp
ios_base& left(ios_base& str);
```

影响：调用 `str.setf(ios_base::left, ios_base::adjustfield)`。

返回值：`str`。

```cpp
ios_base& right(ios_base& str);
```
