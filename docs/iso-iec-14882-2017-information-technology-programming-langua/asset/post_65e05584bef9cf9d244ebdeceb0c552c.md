
# ISO/IEC 14882:2017(E)

## 22.2.10 Class underflow_error

```cpp
namespace std {
    class underflow_error : public runtime_error {
    public:
        explicit underflow_error(const string& what_arg);
        explicit underflow_error(const char* what_arg);
    }
}
```

- 1 The class underflow_error defines the type of objects as exceptions to report an arithmetic underflow error.

```cpp
underflow_error(const string& what_arg);
```

- 2 Effects: Constructs an object of class underflow_error.

- 3 Postconditions: strcmp(what(), what_arg.c_str()) == 0.
```cpp
underflow_error(const char* what_arg);
```

- 4 Effects: Constructs an object of class underflow_error.

- 5 Postconditions: strcmp(what(), what_arg) == 0.

## 22.3 Assertions

- 1 The header <assert> provides a macro for documenting C++ assertions and a mechanism for disabling the assertions.

### 22.3.1 Header <assert> synopsis

```cpp
#define assert(E) see below
```

- 1 The contents are same as the C standard library header <assert.h>, except that a macro named static_assert is not defined.
SEE ALSO: ISO C 7.2

### 22.3.2 The assert macro

- 1 An assert(E) is a constant expression (20.3.6), if
(1.1) NDEBUG is defined at the point where assert is last defined or
(1.2) E contextually converted to bool (Clouse 7) is a constant expression that evaluates to the value true.

## 22.4 Error numbers

- 1 The contents of the header <errno> are same as the POSIX header <errno.h>, except that errno shall be defined as a macro. [Note: The intent is to remain in close alignment with the POSIX standard.] — note A separate errno value is provided for each thread.

### 22.4.1 Header <errno> synopsis

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
#define ENAMOTTYOT see below
#define ENOSPC see below
#define ENGRSR see below
#define EGOTSTR see below
#define ENOTYS see below
#define ENOTCDNN see below
#define ENGTDIR see below
#define ENOTEMPTY see below
#define ENOTREVERABLE see below
#define ENOTCH see below
#define ENOTSUP see below
#define ENUTTY see below
#define ENXIO see below
#define EPDOTSUPP see below
#define EVERFLOW see below
#define EOWNEREAD see below
#define EPERM see below
#define EPIPE see below
#define EPROUT see below
#define ETRONUSSUPPORT see below
#define EPTOTYPE see below
#define ERANAGE see below
#define EDIR see below
#define ESPIPE see below
#define ESRCH see below
#define ETIME see below
#define ETIMEDOUT see below
#define ETBSY see below
#define EWULDBLOCK see below
#define EEDFS see below
```

- 1 The meaning of the macros in header is defined by the POSIX standard.
SEE ALSO: ISO C 7

## 22.5 System error support [syserr]

- 1 This subclause describes components that the standard library and C++ programs may use to report error conditions originating from the operating system or low-level interfaces.
- 2 Components described in this subclause shall not change the value of errno (22.4). Implementations leave the state provided by other libraries unchanged.

### 22.5.1 Header <system_error> synopsis

```cpp
template <class T>
struct is_error_code_enum : false_type {
};

template <class T>
struct is_error_condition_enum : false_type {
};

```cpp
enum errc {
    address_family_not_supported,    // EAFNOSSUPPORT
    address_in_use,                  // EADDRUSE
    address_not_available,           // EADDRAVAIL
    already_connected,               // ECONCONN
    argument_list_too_long,          // EBIG
    argument_out_of_domain,         // ENODATA
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
    too_many_links,                   // EMLINK
    too_many_symbolic_link_levels,    // ELOOP
    value_too_large,                  // EOVERFLOW
    wrong_protocol_type;             // EPROTOTYPE
};

template struct is_error_condition_enum<errc> : true_type { };
```

### 2.2.5.9. non-member functions

```cpp
error_code make_error_code(errc) noexcept;

template <class T, class traits>
basic_operator=(const basic<T, traits>& os, const error_code ec);
```

### 2.2.5.5. non-member functions

```cpp
error_code make_error_condition(errc) noexcept;
```

### 2.2.5.6. comparison functions

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

### 2.2.5.7. hash support

```cpp
template <class T> hash;
template <class T> struct hash_error_code;
template <class T> struct hash_error_condition;
```

### 2.2.5.8. system support

```cpp
template <class T>
inline constexpr bool error_code_enum_v = is_error_condition<T>::value;
template <class T>
inline constexpr bool error_condition_enum_v = is_error_condition<T>::value;
}
```

- 1 The value of each enum errc constant shall be the same as the value of the <errno> macro shown in the above synopsis. Whether or not the <system_error> implementation uses the <errno> macros is specified.
- 2 The is_error_code_enum and is_error_condition_enum may be specialized for user-defined types to indi-
