```
// 20.20.5.3, class template basic_format_parse_context
template<class charT> class basic_format_parse_context;
using format_parse_context = basic_format_parse_context<char>;
using wformat_parse_context = basic_format_parse_context<wchar_t>;

// 20.20.5.4, class template basic_format_context
template<class Out, class charT> class basic_format_context;
using format_context = basic_format_context<unspecified, char>;
using wformat_context = basic_format_context<unspecified, wchar_t>;

// 20.20.6, arguments
// 20.20.6.1, class template basic_format_arg
template<class Context> class basic_format_arg;

template<class Visitor, class Context>
    see below visit_format_arg(Visitor&& vis, basic_format_arg<Context> arg);

// 20.20.6.2, class template format-arg-store
template<class Context, class... Args> struct format-arg-store;      // exposition only

template<class Context = format_context, class... Args>
    format-arg-store<Context, Args...>
    make_format_args(const Args&... args);
template<class... Args>
    format-arg-store<wformat_context, Args...>
    make_wformat_args(const Args&... args);

// 20.20.6.3, class template basic_format_args
template<class Context> class basic_format_args;
using format_args = basic_format_args<format_context>;
using wformat_args = basic_format_args<wformat_context>;

template<class Out, class charT>
    using format_args_t = basic_format_args<basic_format_context<Out, charT>>;

// 20.20.7, class format_error
class format_error;
```

1 The class template format_to_n_result has the template parameters, data members, and special members specified above. It has no base classes or members other than those specified.

# 20.20.2 Format string [format.string]

# 20.20.2.1 In general [format.string.general]

1 A format string for arguments args is a (possibly empty) sequence of replacement fields, escape sequences, and characters other than { and }. Let charT be the character type of the format string. Each character that is not part of a replacement field or an escape sequence is copied unchanged to the output. An escape sequence is one of {{ or }}. It is replaced with { or }, respectively, in the output. The syntax of replacement fields is as follows:

```
replacement-field:
    { arg-id_opt format-specifier_opt }
arg-id:
    0
    positive-integer
positive-integer:
    nonzero-digit
    positive-integer digit
nonnegative-integer:
    digit
    nonnegative-integer digit
```