Our last example of template specialization is the customization of the new `<format>` library introduced in Section 1.7.6 in order to support user types. As before we implemented it with the prototype library `<fmt>` and recommend you to migrate it to `<format>` if it is available on your platform by the time you read this. As an example we choose again the `vector` class for which we like to specify the formatting of the single values. In addition, we want to replace the enclosing brackets with curly braces when the format string contains the letter `'c'`.

To this end, we have to specialize the class `std::formatter` (accordingly `fmt::formatter`). Our specialization shall contain the methods `parse` and `format`. Let's start with the former:

Click here to view code image

```
template <typename Value>
struct formatter<dmc::vector<Value> >
{
    constexpr auto parse(format_parse_context& ctx)
    {
        value_format= "{:";
        for (auto it= begin(ctx); it != end(ctx); ++it) {
            char c= *it;
            if (c == 'c')
                curly= true;
            else
                value_format+= c;
            if (c == '}')
                return it;
        }
        return end(ctx);
    }
    // ...
    bool     curly(false);
    std::string value_format;
};
```

As the argument, the parse context is given whose `begin` iterator points to the first character of the format specification, i.e., the first character after the colon and in its absence the first character after the opening brace. We copy the format specification almost identically to our local `value_format`, only our special character `'c'` is skipped. For simplicity we assume that the