
Table 43 — <errno>

| Type | Name(s) | |
|---|---|---|
| Macros: | ECONNREFUSED | EIO | ENDEV | ENOTEMPT | ERANGE |
| | E2BIG | ECONNRESET | EISSCONN | ENOENT | ENOTCOVERABLE | EROFS |
| | EACCES | EADEADLK | EISDIR | ENOXEC | ENOTSOCK | SPIPE |
| | EDRADDINUSE | EDESTADDREQ | LOOP | ENOLCK | ENOTUPS | ESRCH |
| | EDRNOTAVAIL | EDOM | EMPFILE | ENOLINK | ENOTTY | ETIME |
| | ENOSUPPORT | EEXIST | EMLINK | ENOMEM | ENXIO | ETIMEDOUT |
| | EAGAIN | EFAULT | EMSGSIZE | ENOMOSG | EDNPTSUP | ETIBSY |
| | EALREFBIG | ENAMETOLOONG | ENOPTOUT | EDERFLOW | EWOULDBOCK |
| | EBADSP | EHRONUSTREACH | EDROWN | ENOSPC | EDWINREAD | EXDEV |
| | EBADMSG | EIDRM | EUNETREACH | ENOGSTR | EPERM | errno |
| | EBUSY | EILEQ | ESTR | EPIPE | | |
| | ECANCELED | INPROGRESS | ENOSYS | EPROTO | | |
| | ECHILD | EINTR | ENOBUFS | ENOTCONN | EPROTONUSSUPPORT | | |
| | ECONNABORATED | EINVAL | ENODATA | ENOTDIR | EPROTOTYPE | |

```cpp
class error_condition;

class system_error;

template <Class T>
struct is_error_code_enum : public false_type {};

template <Class T>
struct is_error_condition_enum : public false_type {};

enum class err {
    address_not_supported, // EAFNOSUP
    address_in_use, // EADRADDINUSE
    address_not_available, // EISSCONN
    already_connected, // E2BIG
    argument_list_to_long, // 
    argument_out_of_domain, // EDOM
    bad_address, // EFAULT
    bad_file_descriptor, // EBADF
    bad_message, // EBADMSG
    broken_pipe, // EPIPE
    connection_aborted, // ECONNABORATED
    connection_already_in_progress, // EALREADY
    connection_reset, // ECONNREFUSED
    connection_refused, // ECONNRESET
    cross_device_link, // EXDEV
    destination_address_required, // EDESTADDREQ
    device_or_resource_busy, // EBUSY
    directory_not_entry, // ENOTEMPT
    executable_format_error, // ENOXEC
    file_exists, // EEXIST
    file_too_large, // EFBIG
    filename_to_long, // ENAMETOLOONG
    function_not_supported, // ENOSYS
    boost_unreachable, // EHRONUSTREACH
    identifier_removed // EIDRM
};
```

# ISO/IEC N4296

```cpp
illegal_byte_sequence, // EILSEQ
inappropriate_io_control_operation, // ENDOTTY
interrupted, // EINTR
invalid_argument, // EINVAL
invalid_seek, // EPIPE
io_error, // EIO
is_a_directory, // EISDIR
message_size, // EMSGSIZE
network_down, // ENETOWN
network_reset, // ENETRESET
network_unreachable, // ENUTREACH
no_buffer_space, // ENOBUFS
no_child_process, // ECHILD
no_link, // EOLINK
no_load_available, // ENOLCK
no_message_available, // EDATA
no_message, // EDSMSG
no_protocol_option, // ENOPOPT
no_cm_device, // EISC
no_stream_resources, // ENSR
such_device_or_address, // ENIOX
such_device, // ENDEV
such_file_or_directory, // EROCH
no_process, // ENOTDIR
not_directory, // ENOTDIR
not_socket, // OTSOCK
not_stream, // ENSTR
not_connected, // ENOTCONN
not_memory, // ENOMEM
not_supported, // ENOTSUP
operation_canceled, // ECANCELED
operation_in_progress, // EIPPROGRESS
operation_not_permitted, // EPERM
operation_not_supported, // ENOPSUPP
operation_would_block, // ENOWDBLOCK
owner_dead, // EWOWDEAD
permission_denied, // EACCES
protocol_error, // EOPROTO
protocol_not_supported, // EPROTONSUPP
read_only_file_system, // EROFS
resource_deadlock_would, // EADLEK
resource_unavailable_try_again, // EAGAIN
range_out_of_range, // ERANGE
state_not_recoverable, // ENRECOVERABLE
stream_timeout, // ETIME
file_busy, // ETIMESY
time_out, // ETIMEDOUT
too_many_files_open_in_system, // EMFILE
too_many_files_open, too_many_links, // EMLINK
too_many_symbolic_link_levels, // ELOOP
value_too_large, // EOVER
wrong_protocol_type, // EPROTOTYPE
```

};

§ 19.5

# ISO/IEC N4296

```cpp
template <> struct is_error_code_enum<errc> : true_type { }

error_code make_error_code(errc e) noexcept;

error_code make_error_condition(errc e) noexcept;
```

```cpp
// 19.5.4 比较运算符
bool operator===(const error_code lhs, const error_code rhs) noexcept;
bool operator<=(const error_code lhs, const error_condition rhs) noexcept;
bool operator>=(const error_condition lhs, const error_code rhs) noexcept;
bool operator>=(const error_condition lhs, const error_condition rhs) noexcept;
bool operator!=(const error_code lhs, const error_code rhs) noexcept;
bool operator!=(const error_code lhs, const error_condition rhs) noexcept;
bool operator!=(const error_condition lhs, const error_code rhs) noexcept;
bool operator!=(const error_condition lhs, const error_condition rhs) noexcept;
```

```cpp
// 19.5.5 哈希支持
template <class T> struct hash;
template <class> hash<error_code>;
 // namespace std
```

- 3 每个枚举值的值应与摘要（synopsis）中显示的值相同。无论 `<errno>` 宏是否未指定。
- 4 `is_error_code_enum` 和 `error_condition_enum` 可以针对用户定义类型进行特化，以指示这些类型分别适用于 `error_code` 和 `error_condition` 的自动转换。

## 19.5.1 Class_category [syserrcategory]

### 19.5.1.1 Class_category 概述 [syserrcategory.overview]

`error_category` 用于识别特定类别编码的类型的基类。类可以派生自 `error_category` 以支持除本标准定义的错误之外的类别错误。[注释：`error_category` 对象通过引用传递，如果两个对象具有相同的地址，则它们相等。这意味着使用自定义 `error_category` 类型的应用程序应该创建一个单一对象。]

```cpp
namespace std {
class error_category {
public:
    error_category() noexcept;
    virtual ~error_category();
    error_category(const error_category&) = delete;
    virtual char* name() const noexcept = 0;
    virtual error_condition default_error(int ev) const noexcept;
    virtual bool operator==(const error_code, const error_condition) const noexcept;
    virtual bool operator==(const error_code, int ev) const noexcept;
    virtual std::string message(int ev) const = 0;
    bool operator===(const error_category& rhs) const noexcept;
    bool operator!=(const error_category& rhs) noexcept;
```

### 19.5.1.2 Class_category 虚成员

```cpp
virtual ~error_category();
```
影响：析构 `error_category` 对象。
```cpp
virtual char* name() const noexcept = 0;
```
-：返回类别的名称。
```cpp
virtual error_condition default_error(int ev) const noexcept;
```
- 返回：对应 `ev` 的 `error_condition` 对象。
```cpp
virtual bool operator==(const error_code, const error_condition) const noexcept;
```
- 返回：`this == rhs`。
```cpp
virtual bool operator==(const error_code, int ev) const noexcept;
```
- 返回：`this->value() == ev`。
```cpp
virtual std::string message(int ev) const = 0;
```

### 19.5.1.1 静态成员

```cpp
const error_category& generic_category();
const error_category& system_category();

} // namespace std
```

### 19.5.1.3 Class_category 非虚成员

```cpp
constexpr error_category() noexcept;
```
影响：构造 `error_category` 对象。
```cpp
bool operator==(const error_category& rhs) const noexcept;
```
返回：`this == rhs`。
```cpp
bool operator!=(const error_category& rhs) noexcept;
```
返回：`!rhs`。
```cpp
bool operator<(const error_category& rhs) const noexcept;
```
返回：`this < rhs`。[注释：20.9.6 为指针提供了全序。]

### 19.5.1.4 派生自 error_category 的类

```cpp
virtual char* name() const noexcept = 0;
```
返回：命名类别的字符串。
```cpp
virtual error_condition default_error(int ev) const noexcept;
```
返回：对应 `ev` 的 `error_condition` 对象。
```cpp
virtual bool operator==(const error_code, const error_condition) const noexcept;
```
返回：如果 `this->code() == condition` 则为 `true`，否则为 `false`。
```cpp
virtual bool operator==(const error_code, int ev) const noexcept;
```
返回：如果 `this->value() == ev` 则为 `true`，否则为 `false`。
```cpp
virtual std::string message(int ev) const = 0;
```

## 19.5.5 错误类别对象 [syserr.errcat.objects]

`error_category& generic_category();`

- 返回：派生自 `error_category` 的类型的引用。对此函数的调用应返回相同的对象。

- 注释：`default_error` 和 `equivalent` 虚函数应按照字符串 "generic" 执行。其 `name()` 虚函数返回指向 "generic" 的指针。

`const error_category& system_category();`

- 返回：派生自 `class_category` 的类型的引用。对此函数的调用应返回相同的对象。

- 注释：`equivalent` 虚函数应按照 `class_category` 执行。其 `name()` 虚函数返回指向 "system" 的指针。其 `default_error` 虚函数行为如下：

如果参数返回 POSIX `errno` 值，函数返回 `error_condition(ev, generic_category())`。否则，函数返回 `error_condition(ev, system_category())`。任何给定操作系统的对应关系未定义。[注释：系统错误代码巨大且无边界，某些不对应任何 POSIX `errno` 值。实现在确定对应关系方面具有自由。]

## 19.5.2 Class_code [syserr.errcode]

### 19.5.2.1 Class_code 概述 [syserr.errcode.overview]

`error_code` 类描述用于持有错误代码的对象，这些代码源于操作系统或其他低层应用程序接口。[注释：`error_code` 类是异常报告的辅助。]
