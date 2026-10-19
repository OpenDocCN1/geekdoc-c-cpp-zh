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

template<> struct is_error_condition_enum<errc> : true_type {};

// 19.5.4.5, non-member functions
error_code make_error_code(errc e) noexcept;

template<class charT, class traits>
    basic_ostream<charT, traits>&
        operator<<(basic_ostream<charT, traits>& os, const error_code& ec);

// 19.5.5.5, non-member functions
error_condition make_error_condition(errc e) noexcept;
```