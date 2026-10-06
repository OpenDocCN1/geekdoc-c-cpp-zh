

# ISO/IEC 14882:2017(E)

using system_clock::rep = unspecified;

要求：system_clock::duration::min() < system_clock::duration::zero() 应为真。
[注：这是一个符号类型。] — 结束注

static time_t_to_time_t(const time_t&) noexcept;

返回：一个 time_t 对象，表示与两个值相同的时间点，因为这两个值都受限制为 time_t 和 time_point 中粒度较粗的一个。值是根据所需的精度进行舍入还是截断由实现定义。

static time_point from_time(time_t) noexcept;

返回：一个 time_point 对象，表示与两个值相同的时间点，因为这两个值都受限制为 t 和 time_point 中粒度较粗的一个。由于值是根据所需的精度进行舍入还是截断由实现定义。

## 23.17.2 Steady_clock [time.clock]

类 steady_clock 对象表示时钟，其 time_point 的值随时间的推移永远不会减少，且 time_point 的值增加相对于真实时间的速率。该类可能不可被修改。

```cpp
class steady_clock {
public:
    using rep = unspecified;
    using period = ratio<unspecified, unspecified>;
    using duration = chrono::duration<rep, period>;
    using time_point = chrono::time_point<rep, duration>;
    static const bool is_steady = true;

    static time_point now();
};
```

## 23.17.3 Class high_resolution_clock [time.clock]

类 high_resolution_clock 对象表示具有最短周期的时钟。high_resolution_clock 可能是 system_clock 或 steady_clock 的别名。

```cpp
class high_resolution_clock {
public:
    using rep = unspecified;
    using period = ratio<unspecified, unspecified>;
    using duration = chrono::duration<rep, period>;
    using time_point = chrono::time_point<unspecified, duration>;
    static const bool is_steady = unspecified;

    static time_point now();
};
```

## 23.17.8 Header <ctime> synopsis [ctime]

```cpp
#define NULL 21.2.3
#define CLOCKS_PER_SEC see below
#define TIME_UTC see below
```

```cpp
namespace std {
    using size_t = 21.2.4;
    using clock_t = see below;
    using time_t = see below;
};
```

```cpp
struct timespec;
struct tm;

clock_t clock();
double difftime(time_t t1, time_t t0);
time_t mktime(struct tm* tmptr);
time_t time(time_t* timer, int base);
int timespec_get(struct timespec*, int base);
char* astime(const struct tm* tmptr);
char* ctime(const time_t* timer);
struct tm* gmtime(const time_t* timer);
struct tm* localtime(const time_t* timer);
size_t strftime(char* s, size_t maxsize, const char* format, const struct tm* tm);
}
```

- 1. 头文件 <time> 的内容与 C 库头文件 <time.h> 相同。
- 2. 函数 astime、gmtime 和 localtime 不要求避免数据竞态（20.5.5.9）。

另请：ISO C 7.27

## 23.18 Class type_index [type.index]

### 23.18.1 Header <type_index> synopsis [type.index,synopsis]

```cpp
namespace std {
class type_index;
template<class T> struct hash;
template<class> struct hash<type_index>;
}
```

### 23.18.2 type_index overview [type.index.overview]

```cpp
namespace std {
class type_index {
public:
    type_index&=(const type_index& rhs) const noexcept;
    operator!=(const type_index& rhs) const noexcept;
    operator<(const type_index& rhs) const noexcept;
    operator>(const type_index& rhs) const noexcept;
    operator>=(const type_index& rhs) const noexcept;
    operator<=(const type_index& rhs) const noexcept;

    size_t hash_code() const noexcept;
    const char* name() const noexcept;
private:
    const type_info* info;
// 注意，这里是一个指针的值而不是引用，
// 意味着将提供默认的拷贝/移动构造函数和赋值
// 运算符，并按预期工作。
}
```

- 1. 类 type_index 为 type_info 提供了一个简单的封装，它可以作为关联容器（26.4）和无序关联容器（26.5）中的索引类型。
- 2. strftime 支持 C 转换特殊字符 C, D, e, f, g, h, r, t, u, v, w, 和 z，以及修饰符 E 和 O。

## 23.18.3 type_index members

type_index(const type_info& rhs) noexcept;

- 1. 影响：构造一个 type_index 对象，等同于 target = &rhs。
- 2. bool operator=(const type_index& rhs) const noexcept;
  - 3. bool operator==(const type_index& rhs) const noexcept;
    返回：*rhs。
  - 4. bool operator<(const type_index& rhs) const noexcept;
  - 5. bool operator>(const type_index& rhs) const noexcept;
  - 6. bool operator>=(const type_index& rhs) const noexcept;
  - 7. bool operator<=(const type_index& rhs) const noexcept;

size_t hash_code() const noexcept;
const char* name() const noexcept;

## 23.18.4 Hash support

```cpp
template <> struct hash;
```

- 1. 对于 type_index 对象，hash<type_index> 应等同于 hash_code()。

## 23.19 Execution policies

### 23.19.1 In general

- 1. 此子条款描述了执行策略。执行策略的对象指示算法的并行类型。示例：

```cpp
using namespace std;
vector<int> v;

// 标准排序
sort(v.begin(), v.end());

// 显式顺序
sort(execution::seq, v.begin(), v.end());

// 允许并行
sort(execution::par, v.begin(), v.end());

// 同时允许向量化
sort(execution::par_unseq, v.begin(), v.end());
```
[注：由于并行架构可能需要特殊的参数，实现可以提供此处定义的执行策略。] — 结束注

### 23.19.2 Header <execution> synopsis [execution.syn]

```cpp
namespace std { 
// 23.19.3, 执行策略类型 trait
template<class T> struct is_execution_policy;
template<class T> inline constexpr is_execution_policy_v = is_execution_policy<T>::value;
} namespace std::execution {
// 23.19.4, 顺序执行策略
class sequenced_policy;
// 23.19.5, 并行执行策略
class parallel_policy;
// 23.19.6, 并行无顺序执行策略
class parallel_unsequenced_execution_policy;
// 23.19.7, 执行策略对象
inline constexpr sequenced_policy { seq{ unspecified }; }
inline constexpr parallel_policy { par{ unspecified }; }
inline constexpr parallel_unsequenced_execution_policy { par_unseq{ unspecified }; };
}
```

### 23.19.3 Execution policy type trait [ecpol.type]

- template<class> struct is_execution_policy { see下文 };
is_execution_policy 可用于检测执行策略以便从其他重载解析中排除签名。
is_execution_policy<T> 应是一个 UnaryTypeTrait，如果 T 是标准或实现的执行策略类型，则基础特征为 true_type，否则为 false_type。
[注：此规定为实现保留非标准执行策略的权利。] — 结束注
为 is_execution_policy 添加特化的程序行为是未定义的。

### 23.19.4 Sequenced execution policy [ecpol.seq]

- class execution::sequenced_policy { unspecified };
class execution::sequenced_policy 是一种执行策略，作为唯一类型用于区分并行算法重载，并要求并行算法的执行不能并行化。
在带有 execution::sequenced_policy 的并行算法执行期间，如果元素访问条目通过未捕获的异常退出，则应调用 terminate()。

