You can decide whether you prefer to receive a numeric literal as a preprocessed value or as a sequence of characters. For converting a sequence of 0/1, a character sequence is probably more practical. Preprocessed, the compiler would have passed the decimal number “one hundred eleven” to `operator""_dual`, and we would have had to interpret it in binary with effort. We already saw the template alternative with `operator""_bin`.

Conversely, it is very convenient for `operator""_i` to simply use the constructor of complex that takes a double as an argument. If we had received the literal raw as `const char*`, we would have had to convert it to a number ourselves.

# 23.7.7 Automatically Merged

Merging adjacent literals always carries some risks: Did you just forget the separator, or is it the user's intention to keep the source code nicely formatted? In principle, nothing has changed here because the compiler has always done this task for us.

Only the task has become much more complex due to the many suffixes and prefixes. The rule for strings with user-defined suffixes states something similar to prefixes:

+   - If all strings have the same suffix, the result is unambiguous.
+   - If adjacent strings have different suffixes, it is an error.
+   - If only one of the concatenated strings has a suffix, the entire string is interpreted as if it had that suffix. Which of the strings has the suffix is irrelevant.

The standard provides some examples to illustrate this:

+   - `"A" "B" "C"_x`; becomes `"ABC"_x` when concatenated.
+   - `"P"_x "Q"_y`; results in an error because two different suffixes are used.

# 23.7.8 Unicode Literals

The variants with string length are invoked for literals with the different *encoding prefixes*. That means, depending on `CHAR`, you write this variant:

```
Type operator""_x(const CHAR*, size_t)
```

Which `CHAR` you have to use depends on the *encoding prefix* of your string, as listed in Table 23.2.

Literals in normal and UTF-8 encoding both call

```
operator"" (const char*, size_t)
```

to be interpreted.