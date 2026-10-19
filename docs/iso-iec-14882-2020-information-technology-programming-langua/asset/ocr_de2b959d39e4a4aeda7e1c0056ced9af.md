# ISO/IEC 14882:2020(E)

```
void format(basic_format_parse_context<char_type>& parse_ctx, Context& format_ctx) const;
```

18 Effects: Equivalent to: format_(parse_ctx, format_ctx, ptr_);

```
template<class Visitor, class Context>
  see below visit_format_arg(Visitor&& vis, basic_format_arg<Context> arg);
```

19 Effects: Equivalent to: return visit(forward<Visitor>(vis), arg.value);

# 20.20.6.2 Class template format-arg-store [format.arg.store]

```
namespace std {
  template<class Context, class... Args>
  struct format-arg-store { // exposition only
    array<basic_format_arg<Context>, sizeof...(Args)> args;
  };
}
```

1 An instance of format-arg-store stores formatting arguments.

```
template<class Context = format_context, class... Args>
  format-arg-store<Context, Args...> make_format_args(const Args&... args);
```

2 Preconditions: The type typename Context::template formatter_type<Ti> meets the Formatter requirements (20.20.5.1) for each Ti in Args.

3 Returns: {basic_format_arg<Context>(args)...}.

```
template<class... Args>
  format-arg-store<wformat_context, Args...> make_wformat_args(const Args&... args);
```

4 Effects: Equivalent to: return make_format_args<wformat_context>(args...);

# 20.20.6.3 Class template basic_format_args [format.args]

```
namespace std {
  template<class Context>
  class basic_format_args {
    size_t size_; // exposition only
    const basic_format_arg<Context>* data_; // exposition only
    public:
      basic_format_args() noexcept;
      template<class... Args>
        basic_format_args(const format-arg-store<Context, Args...>& store) noexcept;
      basic_format_arg<Context> get(size_t i) const noexcept;
  };
}
```

1 An instance of basic_format_args provides access to formatting arguments.

```
basic_format_args() noexcept;
```

2 Effects: Initializes size_ with 0.

```
template<class... Args>
  basic_format_args(const format-arg-store<Context, Args...>& store) noexcept;
```

3 Effects: Initializes size_ with sizeof...(Args) and data_ with store.args.data().