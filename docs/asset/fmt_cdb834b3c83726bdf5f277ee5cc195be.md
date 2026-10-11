
```cpp
namespace std {
    class ostream : public basic_ostream<char> {
public:
    ostream();
    ostream(char* s, int n, ios_base::openmode mode = ios_base::out);
    virtual ~ostream();

    streambuf* rdbuf() const;
    void freeze(bool flag = true);
    char* str();
    int count() const;
private:
    streambuf sb; // 仅有
};
```

`ostream` 支持写入 `streambuf` 类对象。它提供一个 `streambuf` 对象来控制关联数组。为了说明，维护的数据展示如下：

- `sb`，`streambuf` 对象。

# D.6.3.1 ostream 构造函数

```cpp
ostream();
```

效果：构造一个 `ostream` 类对象，使用 `ostream(&sb)` 初始化基类，并使用 `streambuf(s)` 初始化 `sb`。

```cpp
ostream(char* s, int n, ios_base::openmode mode = ios_base::out);
```

效果：构造一个 `ostream` 类对象，使用 `ostream(&sb)` 初始化基类，并使用 `streambuf(s)` 初始化：

- (2.1) 如果 `(mode & app) == 0`，`s` 应指定数组的第一个元素。构造函数为 `streambuf(s, n)`。
- (2.2) 如果 `(mode & app) != 0`，`s` 应指定长度为 `n` 的数组的第一个元素。构造函数为 `streambuf(s, n, s + std::strlen(s))`。

(3.3) 位于 `ISO/IEC 14882:2017`

# D.6.3.2 成员函数

```cpp
streambuf* rdbuf() const;
```
返回：`rdbuf()`。

```cpp
void freeze(bool flag = true);
```
效果：调用 `rdbuf()->freeze()`

```cpp
char* str();
```
返回：`rdbuf()->str()`

```cpp
int pcount() const;
```
返回：`rdbuf()->pcount()`.

# D.6.4 类 strstream

```cpp
namespace std {
  class strstream
  : public basic_iostream<char> {
  public:
    // 类型
    using char_type = char;
    using int_type = traits<char>::int_type;
    using pos_type = traits<char>::pos_type;
    using off_type = traits<char>::off_type;
    // 构造函数/析构函数
    strstream();
    strstream(char* s, int n,
      ios_base::openmode mode = ios_base::in|ios_base::out);
    virtual ~strstream();
    // 成员
    streambuf* rdbuf() const;
    void freeze(bool flag = true);
    int pcount() const;
    char* str();
  private:
    streambuf sb; // 仅用于说明
  };
}
```

`strstream` 支持读取和写入 `streambuf` 类对象。它提供一个 `streambuf` 对象来控制关联数组。为了说明，这里展示了：

- `sb`，`streambuf` 对象。

# D.6.4.1 strstream 构造函数

```cpp
strstream();
```
效果：构造一个 `strstream` 类对象，使用 `iostream(sb)` 初始化基类。

```cpp
strstream(char* s, int n,
  ios_base::openmode mode = ios_base::in|ios_base::out);
```

效果：构造一个 `strstream` 类对象，使用 `istream(&sb)` 初始化基类，并使用 `streambuf(s)` 初始化：

- (2.1) 如果 `(mode & app) == 0`，`s` 应指定数组的第一个元素。构造函数为 `streambuf(s, n, s)`。
- (2.2) 如果 `(mode & app) != 0`，`s` 应指定长度为 `n` 的数组的第一个元素。构造函数为 `streambuf(s, n, s + std::strlen(s))`.

# D.6.4.2 strstream 析构函数

```cpp
virtual ~strstream();
```

效果：销毁一个 `strstream` 对象。

# D.6.4.3 strstream 操作

```cpp
streambuf* rdbuf() const;
```
返回：`rdbuf()`。

```cpp
void freeze(bool flag = true);
```

```cpp
char* str();
```
返回：`rdbuf()->str()`。

```cpp
int pcount() const;
```
返回：`rdbuf()->pcount()`.

# D.7 uncaught_exception

头文件 `<exception>` 有：
```cpp
namespace std {
  bool uncaught_exception() noexcept;
}
```
`bool uncaught_exception() noexcept;`
返回：`uncaught_exception() > 0`。

# D.8 旧的可适配绑定

# D.8.1 弱结果类型

包装器可以（23.14.2）具有一个弱结果类型。如果有，其成员 `result_type` 基于包装器的目标对象的类型：

- 如果 `T` 是函数指针，`result_type` 应为 `T` 返回类型的别名；
- 如果 `T` 是成员函数指针，`result_type` 应为 `T` 返回类型的别名；
- 如果 `T` 是类且限定标识 `T:result_type` 有效并表示类型（17.8.2），则 `result_type` 应为 `T::result_type` 的别名；
- 否则不定义 `result_type`。

# D.8.2 支持函数绑定的类型定义

为了使函数适配器能够处理两个或多个参数的对象，本文中的函数对象相应定义了 `argument_type` 和 `result_`



# ISO/IEC 14882:2017(E)

接受一个参数的函数对象的类型，以及接受两个参数的函数对象的 `first_argument_type`、`second_argument_type`, `result_type`。

2 除第 23.14 节指定的名称外，还了以下成员名称：

```cpp
namespace std {
    template<class T> struct owner_less<shared_ptr<T>> {
        using result_type = bool;
        using first_argument_type = shared_ptr<T>;
        using second_argument_type = shared_ptr<T>;
    };
    template<class T> struct owner_less<weak_ptr<T>> {
        using result_type = bool;
        using first_argument_type = weak_ptr<T>;
        using second_argument_type = weak_ptr<T>;
    };
    template<class T> struct reference_wrapper {
public:
        using result_type = see below; // 并不总是定义
        using argument_type = see below; // 并不总是定义
        using first_argument_type = see below; // 并不总是定义
        using second_argument_type = see below; // 并不总是定义
    };
    template<class T> struct plus {
        using first_argument_type = T;
        using second_argument_type = T;
        using result_type = T;
    };
    template<class T> struct minus {
        using first_argument_type = T;
        using second_argument_type = T;
        using result_type = T;
    };
    template<class T> struct multiplies {
        using first_argument_type = T;
        using second_argument_type = T;
        using result_type = T;
    };
    template<class T> struct divides {
        using first_argument_type = T;
        using second_argument_type = T;
        using result_type = T;
    };
    template<class T> struct modulus {
        using first_argument_type = T;
        using second_argument_type = T;
        using result_type = T;
    };
}
```

```cpp
template <class T> struct negate {
    using argument_type = T;
    using result_type = T;
}
```

```cpp
template <class T> struct equal_to {
    using first_argument_type = T;
    using second_argument_type = T;
    using result_type = bool;
}
```

```cpp
template <class T> struct not_equal_to {
    using first_argument_type = T;
    using second_argument_type = T;
    using result_type = bool;
}
```

```cpp
template <class T> struct greater {
    using first_argument_type = T;
    using second_argument_type = T;
    using result_type = bool;
}
```

```cpp
template <class T> struct less {
    using first_argument_type = T;
    using second_argument_type = T;
    using result_type = bool;
}
```

```cpp
template <class T> struct greater_equal {
    using first_argument_type = T;
    using second_argument_type = T;
    using result_type = bool;
}
```

```cpp
template <class T> struct less_equal {
    using first_argument_type = T;
    using second_argument_type = T;
    using result_type = bool;
}
```

```cpp
template <class T> struct logical_and {
    using first_argument_type = T;
    using second_argument_type = T;
    using result_type = bool;
}
```

```cpp
template <class T> struct logical_or {
    using first_argument_type = T;
    using second_argument_type = T;
    using result_type = bool;
}
```

```cpp
template <class T> struct logical_not {
    using argument_type = T;
}
```

```cpp
template <class T> struct bit_and {
    using first_argument_type = T;
    using second_argument_type = T;
    using result_type = bool;
}
```

```cpp
template <class T> struct bit_or {
    using first_argument_type = T;
    using second_argument_type = T;
    using result_type = bool;
}
```

```cpp
template <class T> struct bit_xor {
    using first_argument_type = T;
    using second_argument_type = T;
    using result_type = bool;
}
```

```cpp
template <class T> struct bit_not {
    using argument_type = T;
    using result_type = bool;
}
```

```cpp
template<class R, T1> class function<T1> {
    using argument_type = T1;
};
```

```cpp
template<class R, T1, T2> class function<T1, T2> {
    using first_argument_type = T1;
    using second_argument_type = T2;
};
```
