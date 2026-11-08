The compiler will object to this string literal because the raw literal appears to be terminated somewhere halfway already, right after `(a - b`. But if escaping is not an option—any backslash characters would simply be copied into the raw literal as is—how else can you make it clear to the compiler that the string literal should include this first `)` sequence, as well as the next one after `(b - a`? The answer is that the delimiters that mark the start and end of a raw string literal are flexible. You can use any delimiter of the form `"char_sequence(` to mark the beginning of the literal, as long as you mark the end with a matching sequence `"char_sequence)`. Here's an example:

```
R"*(The answer is "(a - b)" not "(b - a)")*"
```

This is now a valid raw string literal. You can basically choose any `char_sequence` you want, as long as you use the same sequence at both ends:

```
R"=Fa-la-la-la-la"The answer is "(a - b)" not "(b - a)"=Fa-la-la-la-la="
```

The only limitations are that `char_sequence` must not be longer than 16 characters and may not contain any parentheses, spaces, control characters, or backslash characters.

# Summary

In this chapter, you learned how you can use the string type that's defined in the Standard Library. The string type is much easier and safer to use than C-style strings, so it should be your first choice when you need to process character strings.

The following are the important points from this chapter:

+   - The `std::string` type stores a character string.
+   - Like `std::vector<char>`, it is a dynamic array—meaning it will allocate more memory when necessary.
+   - Internally, the terminating null character is still present in the array managed by a `std::string` object, but only for compatibility with legacy and/or C functions. As a user of `std::string`, you normally do not need to know that it even exists. All string functionality transparently deals with this legacy character for you.
+   - You can store string objects in an array or, better still, in a sequence container such as a `vector`.
+   - You can access and modify individual characters in a string object using an index between square brackets. Index values for characters in a string object start at 0.
+   - You can use the `+` operator to concatenate a string object with a string literal, a character, or another string object.
+   - If you want to concatenate a value of one of the fundamental numeric types, such as for instance an int or a double, you must first convert the numeric value into a string. Your easiest—though least flexible—option for this is the `std::to_string()` function template defined in the `<string>` module.
+   - Objects of type string have functions to search, modify, and extract substrings.
+   - The `<string>` module offers functions such as `std::stoi()` and `std::stod()` to convert strings to values of numeric types such as int and double.