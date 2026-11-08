```
```cpp
std::optional<size_t> find_last(const std::string& string, char to_find,
                                std::optional<size_t> start_index)
{
    // code below will not work for empty strings
    if (string.empty())
        return std::nullopt;        // or: 'return std::optional<size_t>{};'
                                    // or: 'return {};'

    // determine the starting index for the loop that follows:
    size_t index = start_index.value_or(string.size() - 1);

    while (true) // never use while (index > 0) here, as size_t is always >= 0!
    {
        if (string[index] == to_find) return index;
        if (index == 0) return std::nullopt;
        --index;
    }
}
```
```

The output produced by this program is as follows:

```
Found the last a at index 46
Found an early i at index 4
```

To showcase `std::optional<>`, we define a variation of the `find_last()` function we used as an example earlier. Notice that because `find_last()` uses unsigned `size_t` indexes instead of `int` indexes, -1 becomes less obvious as a default value for the third parameter. We replaced it with a default value that is equal to `std::nullopt`. This special constant is defined by the Standard Library to initialize `optional<T>` values that do not (yet) have a T value assigned. You will see shortly why this is also a useful default value for function parameters.

After the function's prototype, you see the program's `main()` function. In `main()`, we call `find_last()` three times to search for the letters 'a', 'b', and 'i' in some sample string. And there is really nothing surprising about these calls themselves. If you want a nondefault start index, you simply pass a number to `find_last()`, like we did in our third call. The compiler then implicitly converts this number to a `std::optional<>` object, exactly like you'd expect. If you're okay with the default starting index, though, you can omit the corresponding argument. The default parameter value then takes care of creating an empty optional<>.

These are the two most interesting takeaways from the `main()` function:

+   - How you check whether an `optional<>` value returned by `find_last()` is empty, or whether it was assigned an actual value
+   - How you subsequently extract this value from the `optional<>`

For the former issue, `main()` shows three alternatives, in this order: you have the compiler convert the `optional<>` to a Boolean for you, you call the `has_value()` function, or you compare the `optional<>` to `nullptr`. For the latter issue, `main()` shows two alternatives: you can either use the `*` operator or call the `value()` function. Assigning the `optional<size_t>` return value directly to a `size_t`, however, would not be possible. The compiler cannot convert values of type `optional<size_t>` to values of type `size_t`.

In the body of `find_last()`, aside from some interesting challenges with empty strings and unsigned index types, pay particular attention to two additional aspects related to `optional<>`. First, notice that returning a value is straightforward. Either you return `std::nullopt` or you return an actual value. Both will then be converted to a suitable `optional<>` by the compiler. Second, we've used `value_or()` there.