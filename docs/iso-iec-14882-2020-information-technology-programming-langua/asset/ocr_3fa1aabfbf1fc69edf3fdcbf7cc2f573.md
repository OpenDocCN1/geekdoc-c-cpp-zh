```
std::locale locale();
```

Returns: The locale passed to the formatting function if the latter takes one, and std::locale() otherwise.

```
iterator out();
```

Returns: out_.

```
void advance_to(iterator it);
```

Effects: Equivalent to: out_ = it;

[Example 1:

```
struct S { int value; };

template<> struct std::formatter<S> {
    size_t width_arg_id = 0;

    // Parses a width argument id in the format { digit }.
    constexpr auto parse(format_parse_context& ctx) {
        auto iter = ctx.begin();
        auto get_char = [&]() { return iter != ctx.end() ? *iter : 0; };
        if (get_char() != '{')
            return iter;
        ++iter;
        char c = get_char();
        if (!isdigit(c) || (++iter, get_char()) != '}')
            throw format_error("invalid format");
        width_arg_id = c - '0';
        ctx.check_arg_id(width_arg_id);
        return ++iter;
    }

    // Formats an S with width given by the argument width_arg_id.
    auto format(S s, format_context& ctx) {
        int width = visit_format_arg([](auto value) -> int {
            if constexpr (!is_integral_v<decltype(value)>) 
                throw format_error("width is not integral");
            else if (value < 0 || value > numeric_limits<int>::max())
                throw format_error("invalid width");
            else
                return value;
        }, ctx.arg(width_arg_id));
        return format_to(ctx.out(), "{0:x<{1}}", s.value, width);
    }
};

std::string s = std::format("{0:{1}}", S{42}, 10);  // value of s is "xxxxxxxx42"
```

— end example]

# 20.20.6 Arguments [format.arguments]

# 20.20.6.1 Class template basic_format_arg [format.arg]

```
namespace std {
template<class Context>
class basic_format_arg {
public:
    class handle;

private:
    using char_type = typename Context::char_type;    // exposition only
```