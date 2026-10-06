

# ISO/IEC 14882:2017(E)

## 22.2.10 类 underflow_error

```cpp
namespace std {
    class underflow_error : public runtime_error {
    public:
        explicit underflow_error(const string& what_arg);
        explicit underflow_error(const char* what_arg);
    }
}
```

- 1 类 underflow_error 定义了作为异常的对象的类型，用于报告算术下溢错误。

```cpp
underflow_error(const string& what_arg);
```

- 2 效果：构造一个 underflow_error 类的对象。

- 3 后置条件：strcmp(what(), what_arg.c_str()) == 0。
```cpp
underflow_error(const char* what_arg);
```

- 4 效果：构造一个 underflow_error 类的对象。

- 5 后置条件：strcmp(what(), what_arg) == 0。

## 22.3 断言 (Assertions)

- 1 头文件 <assert> 提供了一个用于记录 C++ 断言的宏，以及一个禁用断言的机制。

### 22.3.1 头文件 <assert> 摘要

```cpp
#define assert(E) see below
```

- 1 内容与 C 标准库头文件 <assert.h> 相同，除了定义名为 static_assert 的宏。
另请参：ISO C 7.2

### 22.3.2 assert 宏

- 1 如果 assert(E) 是一个常量表达式 (20.3.6)，如果：
(1.1) 在 assert 最后定义处定义了 NDEBUG，或者
(1.2) E 在语文中转换为 bool（见从句 7）是一个求值为 true 的常量表达式。

## 22.4 错误代码 (Error numbers)

- 1 头文件 <errno> 的内容与 POSIX 头文件 <errno.h> 相同，但 errno 应定义为宏。[注：意图是与 POSIX 标准保持紧密一致] — 注意：每个线程都提供一个独立的 errno 值。

### 22.4.1 头文件 <errno> 摘要

```cpp
#define errno see below
#define E2BIG see below
#define EACCES see below
#define EADDRINUSE see below
#define EBADNOTAVAIL see below
#define EAFNOSSUPPORT see below
#define EAGAIN see below
#define EALREADY see below
#define EADVF see below
#define EADMSQ see below
#define EBRUSY see below
#define EAMSELED see below
#define ECHID see below
#define ENABORTED see below
#define CONNREFUSED see below
#define ECONNRESET see below
#define EDRALK see below
#define EDESTARRREQ see below
#define EDOM see below
#define EXISTS see below
#define EPARTS see below
#define EFBIG see below
#define EGHOSTUNREACH see below
#define ETDMY see below
#define EIDSLU see below
#define EINPROGRESS see below
#define EINTR see below
#define EINVAL see below
#define EIO see below
#define EISCONN see below
#define EISIDR see below
#define ELODQ see below
#define ENFILE see below
#define EMLINK see below
#define EMSGSIZE see below
#define ENAMETOOLONG see below
#define EETONYC see below
#define EUREST see below
#define ENETUNREACH see below
#define ENFILE see below
#define ENROBYS see below
#define ENDOWIA see below
#define ENODEV see below
#define ENOGENT see below
#define ENORBEC see below
#define ENDOCK see below
#define ENGLINK see below
#define ENOMEM see below
#define ENOMSG see below
#define ENAMOTTY see below
#define ENOSPC see below
#define ENOTYS see below
#define ENGRSR see below
#define EGOTSTR see below
#define ENOTCD see below
#define ENOTYS see below
#define ENOTCH see below
#define ENOTVER see below
#define ENOTSUP see below
#define ENUTTY see below
#define ENXIO see below
#define EPDOT see below
#define EVERFLOW see below
#define ETIMOUT see below
#define EOWNAD see below
#define EPERM see below
#define EODEV see below
#define ETRON see below
#define EPROUT see below
#define EOTUS see below
#define EWULDBLOCK see below
#define EEDADLK see below
#define EAGAIN see below
#define ERANGE see below
#define ENUTRECOVER see below
#define ETIM see below
#define ETRUSY see below
#define TIMEDOUT see below
#define ENFILE see below
#define ENFILE see below
#define EMLINK see below
#define ELOOP see below
#define EOVERFLOW see below
#define EPROTOTYPE 
```

- 1 头文件中宏的含义由 POSIX 标准定义。
另请参：ISO C 7

## 22.5 系统错误支持 [System error]

- 1 此子句描述了标准库和 C++ 程序用于报告来自操作系统或低级接口的错误条件。
- 2 此子句的内容不会改变 errno 的值 (22.4)。

### 22.5.1 头文件 <system_error> 摘要 

```cpp
template <class T>
struct is_error_code : false_type {
};

template <class T>
struct is_error_condition : false_type {
};

```cpp
enum errc {
    address_family_not_supported,    // EAFNOS
    address_in_use,                  // EADDRUSE
    address_not_available,           // EADDVAIL
    already_connected,               // ECONCONN
    argument_list_too_long,          // EBIG
    argument_out_domain,         // ENODATA
    bad_address,                     // EFAULT
    bad_file_descriptor,             // EBADF
    bad_message,                     // EBADMSG
    broken_pipe,                     // EPIPE,
    connection_aborted,              // ENABORT
    connection_already_in_progress, // EALREADY
    connection_refused,             // ENREFUSED
    connection_reset,                // ENRESET
    cross_device,                    // EODEV
    destination_address_required,    // EADDRREQ
    device_or_resource_busy,         // EBUSY
    directory_not_empty,             // ENOTEMPTY
    executable_format_error,         // ENOEXEC
    file_exists,                     // EEXIST
    file_too_large,                  // EFSFS
    filename,                        // ENAMETOLONG
    function_not_supported,          // ENOTSUP
    host_unreachable,                // EGUNREACH
    identifier_removed,              // EIDM
    illegal_base_sequence,           // EISEQ
    inappropriate_io_control,        // ENUTTY
    interrupted,                     // EINTR
    invalid_argument,                // EINVAL
    invalid_seek,                    // EISPE
    io_error,                        // EIO
    is_a_directory,                  // ENDIR
    message_size,                    // EMSGSIZE
    network_down,                    // ENEDOWN
    network_reset,                   // ENRESET
    network_unreachable,             // ENOTREACH
    no_buffer_space,                 // ENOPC
    no_child,                        // ECHILD
    no_link,                         // ENOLINK
    no_lock_available,               // ELOCK
    no_media_available,              // ENMEDIA
    no_message,                      // ENOMSG
    no_protocol_option,              // ENOPTO
    no_space_on_device,              // ENOSPC
    no_resource,                     // EROFS
    no_such_device,                  // ENODEV
    no_file_or_directory,            // ENOEST
    no_process,                      // ENOCH
    not_a_directory,                 // ENUTDIR
    not_a_socket,                    // OTSOCK
    not_connected,                   // ECONN
    not_enough_memory,               // ENOMEM
    not_supported,                   // ENOTSUP
    operation_canceled,               // ECANCE
    operation_in_progress,           // EPROGRESS
    operation_not_permitted,         // EPERM
    operation_not_supported,         // EOPROTSUP
    operation_would_block,            // EWOULDBLOCK
    resource_deadlock_would_occur,    // EEDADLK
    resource_unavailable_try_again,  // EAGAIN
    result_out_range,                // ERANGE
    state_not_recoverable,           // ENUTRECOVER
    stream_timeout,                   // ETIM
    is_busy,                         // ETRUSY
    timed_out,                       // TIMEDOUT
    too_many_files_open_in_system,    // ENFILE
    too_many_files_open,               // ENFILE
    too_many_links,                 // EMLINK
    too_many_symbolic_link_levels,    // ELOOP
    value_too_large,                  // EOVERFLOW
    wrong_protocol_type;             // EPROTOTYPE
};

template struct is_error_code_enum<errc> : true_type { };
```

### 22.5.9 非成员函数

```cpp
error_code make_error_code(errc) noexcept;

template <class T, class traits>
basic_operator=(const basic<T, traits>& os, const error_code ec);
```

### 22.5.5 非成员函数

```cpp
error_code make_error_condition(errc) noexcept;
```

### 22.5.6 比较函数

```cpp
bool operator==(const error_code lhs, const error_code rhs) noexcept;
bool operator!=(const error_code lhs, const error_code rhs) noexcept;
bool operator<=(const error_code lhs, const error_code rhs) noexcept;
bool operator>(const error_code lhs, const error_code rhs) noexcept;
bool operator<=(const error_code lhs, const error_code rhs) noexcept;
bool operator>=(const error_code lhs, const error_code rhs) noexcept;
bool operator!=(const error_code lhs, const error_code rhs) noexcept;
bool operator!=(const error_code lhs, const error_code rhs) noexcept;
```

### 22.5.7 哈希支持

```cpp
template <class T> hash;
template <class T> struct hash_error_code;
template <class T> struct hash_error_condition;
```

### 22.5.8 系统支持

```cpp
template <class T>
inline constexpr bool error_code_enum_v = is_error_condition<T>::value;
template <class T>
inline constexpr bool error_condition_enum_v = is_error_condition<T>::value;
}
```

