

## ISO/IEC 14882:2020(E)

3 [示例 1：

```
struct s {
    source_location member = source_location::current();
    int other_member;
    s(source_location loc = source_location::current())
        : member(loc)                // values of member refer to the location of the calling function (9.3.4.7)
    {}
    s(int blather) :            // values of member refer to this location
        other_member(blather)
    {}
    s(double)                   // values of member refer to this location
    {}
};
void f(source_location a = source_location::current()) {
    source_location b = source_location::current();      // values in b refer to this line
}

void g() {
    f();                            // f's first argument corresponds to this line of code

    source_location c = source_location::current();
    f(c);                           // f's first argument gets the same values as c, above
}
```

--- 结束示例]

```
constexpr source_location() noexcept;
```

4 效果：数据成员以有效但未指定的值初始化。

### 17.8.2.3 观察者 [support.src.loc.obs]

```
constexpr uint_least32_t line() const noexcept;
```

1 返回：line_。

```
constexpr uint_least32_t column() const noexcept;
```

2 返回：column_。

```
constexpr const char* file_name() const noexcept;
```

3 返回：file_name_。

```
constexpr const char* function_name() const noexcept;
```

4 返回：function_name_。

### 17.9 异常处理 [support.exception]

### 17.9.1 概述 [support.exception.general]

1 头文件 <exception> 定义了与 C++ 程序中的异常处理相关的若干类型和函数。

### 17.9.2 头文件 <exception> 概要 [exception.syn]

```
namespace std {
    class exception;
    class bad_exception;
    class nested_exception;

    using terminate_handler = void (* )();
    terminate_handler get_terminate() noexcept;
    terminate_handler set_terminate(terminate_handler f) noexcept;
    [[noreturn]] void terminate() noexcept;

    int uncaught_exceptions() noexcept;

    using exception_ptr = unspecified;
    exception_ptr current_exception() noexcept;
    [[noreturn]] void rethrow_exception(exception_ptr p);
    template<class E> exception_ptr make_exception_ptr(E e) noexcept;

    template<class T> [[noreturn]] void throw_with_nested(T&& t);
    template<class E> void rethrow_if_nested(const E& e);
}
```

### 17.9.3 类 exception

```
namespace std {
  class exception {
  public:
    exception() noexcept;
    exception(const exception&) noexcept;
    exception& operator=(const exception&) noexcept;
    virtual ~exception();
    virtual const char* what() const noexcept;
  };
}
```

类 exception 定义了 C++ 标准库组件和某些表达式作为异常抛出的对象类型的基类，以报告程序执行期间检测到的错误。

每个从类 exception 派生的标准库类 T 都具有以下可公开访问的成员函数，且每个函数都具有不抛出异常的异常规约（14.5）：

- (2.1) — 默认构造函数（除非类概要中显示了其他构造函数）
- (2.2) — 复制构造函数
- (2.3) — 复制赋值运算符

复制构造函数和复制赋值运算符满足以下后置条件：如果两个对象 lhs 和 rhs 都具有动态类型 T，且 lhs 是 rhs 的副本，则 strcmp(lhs.what(), rhs.what()) 等于 0。每个此类 T 的 what() 成员函数都满足为 exception::what() 指定的约束（见下文）。

```
exception(const exception& rhs) noexcept;
exception& operator=(const exception& rhs) noexcept;
```

后置条件：如果 *this 和 rhs 都具有动态类型 exception，则表达式 strcmp(what(), rhs.what()) 的值应等于 0。

```
virtual ~exception();
```

效果：销毁类 exception 的对象。

```
virtual const char* what() const noexcept;
```

返回：实现定义的 NTBS。

备注：该消息可以是一个以空字符结尾的多字节字符串（16.3.3.5.3），适合转换并显示为 wstring（21.3, 28.4.2.5）。返回值一直有效，直到获取它的异常对象被销毁或调用该异常对象的非常量成员函数为止。

### 17.9.4 类 bad_exception

```
namespace std {
  class bad_exception : public exception {
  public:
    // see 17.9.3 for the specification of the special member functions
    const char* what() const noexcept override;
  };
}
```

类 bad_exception 定义了当当前活动异常对象无法复制时，由调用 current_exception（17.9.7）返回的 exception_ptr 所引用的对象的类型。

```
const char* what() const noexcept override;
```

返回：实现定义的 NTBS。

### 17.10 初始化列表 [support.initlist]

### 17.10.1 概述 [support.initlist.general]

1 头文件 <initializer_list> 定义了一个类模板和几个与列表初始化相关的支持函数（见 9.4.5）。17.10 中指定的所有函数均为信号安全函数（17.13.5）。

### 17.10.2 头文件 <initializer_list> 概要 [initializer.list.syn]

```
namespace std {
template<class E> class initializer_list {
public:
using value_type = E;
using reference = const E&;
using const_reference = const E&;
using size_type = size_t;
using iterator = const E*;
using const_iterator = const E*;
constexpr initializer_list() noexcept;
constexpr size_t size() const noexcept; // number of elements
constexpr const E* begin() const noexcept; // first element
constexpr const E* end() const noexcept; // one past the last element
};
// 17.10.5, initializer list range access
template<class E> constexpr const E* begin(initializer_list<E> il) noexcept;
template<class E> constexpr const E* end(initializer_list<E> il) noexcept;
}
```

1 initializer_list<E> 类型的对象提供对 const E 类型对象数组的访问。

> [注 1：一对指针或一个指针加上一个长度是 initializer_list 的明显表示方式。initializer_list 用于实现 9.4.5 中指定的初始化列表。复制初始化列表不会复制底层元素。— 结束注]

2 如果声明了 initializer_list 的显式特化或部分特化，则程序是非良构的。

```
[[noreturn]] void rethrow_nested() const;
```

效果：如果 nested_ptr() 返回空指针，则该函数调用函数 std::terminate。否则，它抛出 *this 捕获的存储异常。

```
exception_ptr nested_ptr() const noexcept;
```

返回：此 nested_exception 对象捕获的存储异常。

```
template<class T> [[noreturn]] void throw_with_nested(T&& t);
```

设 U 为 decay_t<T>。

前置条件：U 满足 Cpp17CopyConstructible 要求。

抛出：如果 is_class_v<U> && !is_final_v<U> && !is_base_of_v<nested_exception, U> 为 true，则抛出一种未指定类型的异常，该异常公开派生自 U 和 nested_exception，并由 std::forward<T>(t) 构造；否则抛出 std::forward<T>(t)。

```
template<class E> void rethrow_if_nested(const E& e);
```

效果：如果 E 不是多态类类型，或者 nested_exception 是 E 的不可访问或歧义基类，则没有任何效果。否则，执行以下操作：

```
if (auto p = dynamic_cast<const nested_exception*>(addressof(e)))
    p->rethrow_nested();
```

### 17.10.3 初始化列表构造函数 [support.initlist.cons]

```
constexpr initializer_list() noexcept;
```

后置条件：size() == 0。

### 17.10.4 初始化列表访问 [support.initlist.access]

```
constexpr const E* begin() const noexcept;
```

返回：指向数组开头的指针。如果 size() == 0，则 begin() 和 end() 的值未指定，但它们必须相同。

```
constexpr const E* end() const noexcept;
```

返回：begin() + size()。

```
constexpr size_t size() const noexcept;
```

返回：数组中的元素数量。

复杂度：常数时间。

### 17.10.5 初始化列表范围访问 [support.initlist.range]

```
template<class E> constexpr const E* begin(initializer_list<E> il) noexcept;
```

返回：il.begin()。

```
template<class E> constexpr const E* end(initializer_list<E> il) noexcept;
```

返回：il.end()。

### 17.11 比较 [cmp]

### 17.11.1 头文件 <compare> 概要 [compare.syn]

头文件 <compare> 规定了主要与三路比较运算符（7.6.8）一起使用的类型、对象和函数。

```
namespace std {
  // 17.11.2, comparison category types
  class partial_ordering;
  class weak_ordering;
  class strong_ordering;

  // named comparison functions
  constexpr bool is_eq (partial_ordering cmp) noexcept { return cmp == 0; }
  constexpr bool is_neq (partial_ordering cmp) noexcept { return cmp != 0; }
  constexpr bool is_lt (partial_ordering cmp) noexcept { return cmp < 0; }
  constexpr bool is_lteq(partial_ordering cmp) noexcept { return cmp <= 0; }
  constexpr bool is_gt (partial_ordering cmp) noexcept { return cmp > 0; }
  constexpr bool is_gteq(partial_ordering cmp) noexcept { return cmp >= 0; }

  // 17.11.3, common comparison category type
  template<class... Ts>
  struct common_comparison_category {
    using type = see below;
  };
  template<class... Ts>
  using common_comparison_category_t = typename common_comparison_category<Ts...>::type;

  // 17.11.4, concept three_way_comparable
  template<class T, class Cat = partial_ordering>
    concept three_way_comparable = see below;
  template<class T, class U, class Cat = partial_ordering>
    concept three_way_comparable_with = see below;

  // 17.11.5, result of three-way comparison
  template<class T, class U = T> struct compare_three_way_result;
```

