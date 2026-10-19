
## 18.7.6 Concept equivalence_relation [concept.equiv]

```
template<class R, class T, class U>
concept equivalence_relation = relation<R, T, U>;
```

1 A relation models equivalence_relation only if it imposes an equivalence relation on its arguments.

## 18.7.7 Concept strict_weak_order [concept.strictweakorder]

```
template<class R, class T, class U>
concept strict_weak_order = relation<R, T, U>;
```

1 A relation models strict_weak_order only if it imposes a strict weak ordering on its arguments.

2 The term strict refers to the requirement of an irreflexive relation (!comp(x, x) for all x), and the term weak to requirements that are not as strong as those for a total ordering, but stronger than those for a partial ordering. If we define equiv(a, b) as !comp(a, b) && !comp(b, a), then the requirements are that comp and equiv both be transitive relations:

- (2.1) — comp(a, b) && comp(b, c) implies comp(a, c)
- (2.2) — equiv(a, b) && equiv(b, c) implies equiv(a, c)

3 [Note 1: Under these conditions, it can be shown that

- (3.1) — equiv is an equivalence relation,
- (3.2) — comp induces a well-defined relation on the equivalence classes determined by equiv, and
- (3.3) — the induced relation is a strict total ordering.

— end note]

## 19 Diagnostics library [diagnostics]

### 19.1 General [diagnostics.general]

1 This Clause describes components that C++ programs may use to detect and report error conditions.

2 The following subclauses describe components for reporting several kinds of exceptional conditions, documenting program assertions, and a global variable for error number codes, as summarized in Table 40.

Table 40: Diagnostics library summary [tab:diagnostics.summary]

| Subclause | Header |
|---|---|
| 19.2 | Exception classes | <stdexcept> |
| 19.3 | Assertions | <cassert> |
| 19.4 | Error numbers | <cerrno> |
| 19.5 | System error support | <system_error> |

### 19.2 Exception classes [std.exceptions]

#### 19.2.1 General [std.exceptions.general]

1 The C++ standard library provides classes to be used to report certain errors (16.4.6.13) in C++ programs. In the error model reflected in these classes, errors are divided into two broad categories: logic errors and runtime errors.

2 The distinguishing characteristic of logic errors is that they are due to errors in the internal logic of the program. In theory, they are preventable.

3 By contrast, runtime errors are due to events beyond the scope of the program. They cannot be easily predicted in advance. The header <stdexcept> defines several types of predefined exceptions for reporting errors in a C++ program. These exceptions are related by inheritance.

#### 19.2.2 Header <stdexcept> synopsis [stdexcept.syn]

```
namespace std {
    class logic_error;
    class domain_error;
    class invalid_argument;
    class length_error;
    class out_of_range;
    class runtime_error;
    class range_error;
    class overflow_error;
    class underflow_error;
}
```

#### 19.2.3 Class logic_error [logic.error]

```
namespace std {
    class logic_error : public exception {
    public:
        explicit logic_error(const string& what_arg);
        explicit logic_error(const char* what_arg);
    };
}
```

1 The class logic_error defines the type of objects thrown as exceptions to report errors presumably detectable before the program executes, such as violations of logical preconditions or class invariants.

```
logic_error(const string& what_arg);
```

2 Postconditions: strcmp(what(), what_arg.c_str()) == 0.

};
}

1 The class out_of_range defines the type of objects thrown as exceptions to report an argument value not in its expected range.

```
out_of_range(const string& what_arg);
```

2 Postconditions: strcmp(what(), what_arg.c_str()) == 0.

```
out_of_range(const char* what_arg);
```

3 Postconditions: strcmp(what(), what_arg) == 0.

#### 19.2.8 Class runtime_error [runtime.error]

```
namespace std {
  class runtime_error : public exception {
  public:
    explicit runtime_error(const string& what_arg);
    explicit runtime_error(const char* what_arg);
  };
}
```

1 The class runtime_error defines the type of objects thrown as exceptions to report errors presumably detectable only when the program executes.

```
runtime_error(const string& what_arg);
```

2 Postconditions: strcmp(what(), what_arg.c_str()) == 0.

```
runtime_error(const char* what_arg);
```

3 Postconditions: strcmp(what(), what_arg) == 0.

#### 19.2.9 Class range_error [range.error]

```
namespace std {
  class range_error : public runtime_error {
  public:
    explicit range_error(const string& what_arg);
    explicit range_error(const char* what_arg);
  };
}
```

1 The class range_error defines the type of objects thrown as exceptions to report range errors in internal computations.

```
range_error(const string& what_arg);
```

2 Postconditions: strcmp(what(), what_arg.c_str()) == 0.

```
range_error(const char* what_arg);
```

3 Postconditions: strcmp(what(), what_arg) == 0.

#### 19.2.10 Class overflow_error [overflow.error]

```
namespace std {
  class overflow_error : public runtime_error {
  public:
    explicit overflow_error(const string& what_arg);
    explicit overflow_error(const char* what_arg);
  };
}
```

1 The class overflow_error defines the type of objects thrown as exceptions to report an arithmetic overflow error.

```
overflow_error(const string& what_arg);
```

2 Postconditions: strcmp(what(), what_arg.c_str()) == 0.

```
#define ECANCELED see below
#define ECHILD see below
#define ECONNABORTED see below
#define ECONNREFUSED see below
#define ECONNRESET see below
#define EDEADLK see below
#define EDESTADDRREQ see below
#define EDOM see below
#define EEXIST see below
#define EFAULT see below
#define EFBIG see below
#define EHOSTUNREACH see below
#define EIDRM see below
#define EILSEQ see below
#define EINPROGRESS see below
#define EINTR see below
#define EINVAL see below
#define EIO see below
#define EISCONN see below
#define EISDIR see below
#define ELOOP see below
#define EMFILE see below
#define EMLINK see below
#define EMSGSIZE see below
#define ENAMETOOLONG see below
#define ENETDOWN see below
#define ENETRESET see below
#define ENETUNREACH see below
#define ENFILE see below
#define ENOBUFS see below
#define ENODATA see below
#define ENODEV see below
#define ENOENT see below
#define ENOEXEC see below
#define ENOLCK see below
#define ENOLINK see below
#define ENOMEM see below
#define ENOMSG see below
#define ENOPROTOOPT see below
#define ENOSPC see below
#define ENOSR see below
#define ENOSTR see below
#define ENOSYS see below
#define ENOTCONN see below
#define ENOTDIR see below
#define ENOTEMPTY see below
#define ENOTRECOVERABLE see below
#define ENOTSOCK see below
#define ENOTSUP see below
#define ENOTTY see below
#define ENXIO see below
#define EOPNOTSUPP see below
#define EOVERFLOW see below
#define EOWNERDEAD see below
#define EPERM see below
#define EPIPE see below
#define EPROTO see below
#define EPROTONOSUPPORT see below
#define EPROTOTYPE see below
#define ERANGE see below
#define EROFS see below
#define ESPIPE see below
#define ESRCH see below
#define ETIME see below

```
invalid_argument,                  // EINVAL
invalid_seek,                      // ESPIPE
io_error,                          // EIO
is_a_directory,                    // EISDIR
message_size,                      // EMSGSIZE
network_down,                      // ENETDOWN
network_reset,                     // ENETRESET
network_unreachable,               // ENETUNREACH
no_buffer_space,                   // ENOBUFS
no_child_process,                  // ECHILD
no_link,                           // ENOLINK
no_lock_available,                 // ENOLCK
no_message_available,              // ENODATA
no_message,                        // ENOMSG
no_protocol_option,                // ENOPROTOOPT
no_space_on_device,                // ENOSPC
no_stream_resources,               // ENOSR
no_such_device_or_address,         // ENXIO
no_such_device,                    // ENODEV
no_such_file_or_directory,         // ENOENT
no_such_process,                   // ESRCH
not_a_directory,                   // ENOTDIR
not_a_socket,                      // ENOTSOCK
not_a_stream,                      // ENOSTR
not_connected,                     // ENOTCONN
not_enough_memory,                 // ENOMEM
not_supported,                     // ENOTSUP
operation_canceled,                // ECANCELED
operation_in_progress,             // EINPROGRESS
operation_not_permitted,           // EPERM
operation_not_supported,           // EOPNOTSUPP
operation_would_block,             // EWOULDBLOCK
owner_dead,                        // EOWNERDEAD
permission_denied,                 // EACCES
protocol_error,                    // EPROTO
protocol_not_supported,            // EPROTONOSUPPORT
read_only_file_system,             // EROFS
resource_deadlock_would_occur,     // EDEADLK
resource_unavailable_try_again,    // EAGAIN
result_out_of_range,               // ERANGE
state_not_recoverable,             // ENOTRECOVERABLE
stream_timeout,                    // ETIME
text_file_busy,                    // ETXTBSY
timed_out,                         // ETIMEDOUT
too_many_files_open_in_system,     // ENFILE
too_many_files_open,               // EMFILE
too_many_links,                    // EMLINK
too_many_symbolic_link_levels,     // ELOOP
value_too_large,                   // EOVERFLOW
wrong_protocol_type,               // EPROTOTYPE
};
```

template<> struct is_error_condition_enum<errc> : true_type {};

// 19.5.4.5, non-member functions
error_code make_error_code(errc e) noexcept;

template<class charT, class traits>
    basic_ostream<charT, traits>&
        operator<<(basic_ostream<charT, traits>& os, const error_code& ec);

// 19.5.5.5, non-member functions
error_condition make_error_condition(errc e) noexcept;
