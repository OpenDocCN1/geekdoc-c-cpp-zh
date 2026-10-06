

# ISO/IEC 14882:2017(E)

指针。
备注：当 placement new 表达式中初始化的任何部分调用了库的非数组 placement operator new 时，将通过抛出异常终止 (8.3.4)。这是调用的默认函数。

```cpp
void operator delete[](void* ptr, void*) noexcept;
```

影响：刻意不执行任何操作。

要求：如果初始化具有严格的指针安全性 (6.7.4.3)，则 ptr 应该是安全派生指针（safely-derived pointer）。

当 placement new 表达式中初始化的任何部分调用了库的数组 placement operator new 时，将通过抛出异常终止 (8.3.4)。这是调用的默认函数。

## 21.6.2.4 数据竞



 为了确定数据竞态的存在，operator new 的库版本、全局 operator new 的替换版本、C 标准库函数 `aligned_alloc`、`calloc` 和 `malloc`；operator delete 的库版本、operator delete 的替换版本、C 标准库 `free` 和 C 标准库 `alloc` 不得引入数据竞态 (20.5.9)。对特定存储进行分配和释放的所有调用都发生在单一总序中，且每次释放都应发生在该顺序中 (4.7) 下一次分配（如果有）之前。

## 21.6.3 存储分配错误

### 21.6.3.1 类 bad_alloc

```cpp
namespace std {
    class bad_alloc : public exception {
    public:
        bad_alloc() noexcept;
        bad_alloc(const bad_alloc&) noexcept;
        bad_alloc& operator=(const bad_alloc&) noexcept;
        virtual const char* what() const noexcept override;
    };
};
```

- 类 bad_alloc 定义了实现通过抛出异常来报告的对象类型，用于报告存储分配失败。

```cpp
bad_alloc() noexcept;
```

影响：构造一个 bad_alloc 类的对象。

```cpp
bad_alloc(const bad_alloc&) noexcept;
bad_alloc& operator=(const bad_alloc&) noexcept;
```

影响：拷贝一个 bad_alloc 类的对象。

```cpp
const char* what() const noexcept override;
```

返回：一个实现定义的 NTBS（空空字符字符串）。

备注：消息可能是多字节字符串 (20.4.2.15.2)，适合转换并显示为 wstring (24.3, 25.4.1.4)。

### 21.6.3.2 类 bad_array_new_length

```cpp
namespace std {
    class bad_array_new_length : public bad_alloc {
    public:
        bad_array_new_length() noexcept;
        virtual const char* what() const noexcept override;
    };
};
```

类 bad_array_new_length 定义了实现通过抛出异常来报告的对象类型，用于报告分配的数组大小小于或大于实现的限制 (8.3.4)。

```cpp
bad_array_new_length() : noexcept;
```

影响：构造一个 bad_array_new_length 类的对象。

```cpp
const char* what() const noexcept override;
```

返回：一个实现定义的 NTBS。

备注：消息可能是非多字节字符串 (20.4.2.1.5.2)，适合转换并显示为宽字符串 (24.3, 25.4.1.4)。

### 21.6.3.3 类型 new-handler [new.handler]

```cpp
using new_handler = void (*)();
```

- 当 operator new() 或 operator new[] (21.6.2) 无法满足额外存储的请求时，调用的处理函数类型。

- 强制行为：new-handler 应当执行以下操作之一：
  (2.1) 确保有可分配的存储并返回；
  (2.2) 抛出 bad_alloc 类型或派自 bad_alloc 的类的异常；
  (2.3) 终止程序的执行而不返回给调用者。

### 21.6.3.4 set new-handler [new.handler]

```cpp
new_handler set_new_handler(new_handler new_p) noexcept;
```

影响：将由 new_p 指定的设为当前的 new-handler。

返回：之前的 new-handler。

备注：初始的 new-handler 是空指针。

### 21.6.3.5 get_new-handler [new.handler]

```cpp
new_handler get_new_handler() noexcept;
```

返回：当前的 new-handler。[注：这可能为空值。]

## 21.6.4 指针优化屏障 [ptr.launder]

```cpp
template <class T> T* launder(T* p) noexcept;
```

- 要求：p 代表内存中某个字节的地址 A。在其生命周期内 (6.8) 的对象 X 的类型与 T 相似 (7.5)，位于地址 A。所有通过结果可达的类型存储都是可达的（见下文）。

- 返回：一个指向 X 的 T* 类型值。

- 备注：当参数的值在常量表达式中使用时，此函数的调用可以在常量表达式中使用。一个通过指向对象 Y 的指针可达的类型存储，如果它位于 X 占据的存储内，或者与 Y 指针可转换，或者如果 Y 是数组元素，则位于紧邻的数组对象内。如果 T 是数组或 void，则程序是格式错误的。

注意：如果在现有相同类型对象占据的存储中创建了新对象，可以使用指向原始对象的指针来引用该对象，除非该类型包含 const 或引用成员；在后的情况下，可以使用此函数获取指向新对象的指针。见 6.8。

示例：

```cpp
struct X { const int n; };
X *p = new X(3);
const int a = p->n; // p 不指向对象 (6.8)，因为 X::n 是 const
const int b = p->n; // 未定义行为
const int c = std::launder(p)->n; // OK
```

## 21.6.5 硬件干扰尺寸

```cpp
inline size_t hardware_interference_size;
```

该数字是并发访问的对象对象之间的最小尺寸，以避免因竞争导致性能下降。它应该至少为 `alignof(max_t)`。

## 21.7 类型识别

### 21.7.1 头文件 <typeinfo> 摘要

```cpp
namespace std {
    class type_info;
    class bad_cast;
}
```

### 21.7.2 类 type_info [type.info]

```cpp
namespace std {
    class type_info {
    public:
        virtual ~type_info() noexcept;
        bool operator==(const type_info& rhs) const noexcept;
        bool operator!(const type_info& rhs) const noexcept;
        bool before(const type_info& rhs) const noexcept;
        size_t hash_code() const noexcept;
        virtual const char* name() const noexcept;
    };
}
```

- 类 type_info 描述实现生成的类型信息 (8.2)。此类的对象存储指向名称的指针和一个用于比较类型的编码。名称、编码和调用序列都是未指定的并随程序而异。

- bool operator==(const type_info& rhs) const noexcept;
  影响：比较当前对象与 rhs。
  返回：如果两个值描述相同的类型。

- operator!(const type_info& rhs) const noexcept;
  返回：(*this == rhs)。

- bool before(const type_info& rhs) const noexcept;
  影响：比较当前对象与 rhs。
  返回：如果 *this 在实现的排序顺序中先于 rhs。

- size_t hash_code() const noexcept;
  返回：一个未指定的值，但在程序的单执行期间，对于任何两个相等的 type_info 对象应返回相同的值。
  备注：实现可以对不相等的 type_info 对象返回不同的值。

- const char* name() const noexcept;
  返回：一个实现定义的 NTBS。
  备注：消息可能是空终止的多字节字符串 (20.4.2.1.5.2)，适合转换并显示为 (24.3, 25.4.1.4)。

- type_info(const type_info& rhs) = delete;
- type_info& operator=(const type_info& rhs) = delete;

