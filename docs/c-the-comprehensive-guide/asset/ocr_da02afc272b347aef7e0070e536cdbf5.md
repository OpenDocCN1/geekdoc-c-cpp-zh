The standard input/output operators support almost all fundamental types in C++. Exceptions are `void` and `nullptr_t`. Of course, input and output do not occur arbitrarily. There are also a few things you need to consider:

+   - **Numeric types**
+     When reading a numeric value, the input must start with at least one digit. If you specify the sign with `+` or `-`, it must only appear before the first digit. However, there must be no space between the sign and the digit. Leading whitespace characters are ignored. In case of an erroneous input, the numeric value is set to 0 and `std::failbit` is set.

+   - **`char*`**
+     The use of `char*` for input was already very critical in C. Input is read until the first whitespace or until *end of file* (EOF; more on this later). Leading whitespace is skipped, which can be changed with the `skipws` manipulator. The problem with reading `char*` is that it can read beyond the buffer area (buffer overflow)—for example, `char cval[20]; std::cin >> cval`. If you read in more than 20 characters here, `cin` will dutifully do so and write into an undefined memory area. Therefore, with old C-strings (if you absolutely must use them), you must always ensure that the maximum length is not exceeded. For this, the `setw` manipulator from the `<iomanip>` header is suitable—for example, `cin >> setw(20) >> cval`.

+   - **bool**
+     The output of `bool` is converted to 0 for `false` and to 1 for `true`. For input, the same rules as for numeric values apply initially. When entering valid numeric values other than 0, it is converted to 1 (`=true`). When entering 0 (0 for `false`) is used. In case of an erroneous input, the value is also set to 0 and `std::failbit`.

# 27.3 Methods for Stream Input and Output

In addition to the usual `operator<<` and `operator>>` for streams, you can also use methods provided by the I/O stream library. However, unlike the << and >> operators, these methods work with raw bytes and are therefore unformatted. The methods for standard input/output use the `streamsize` type from `<ios>`, which is usually `size_t`. This means, for example, that leading whitespace is not ignored during input.

# 27.3.1 Methods for Unformatted Output

For raw and unformatted output, the I/O stream library provides the `put()` and `write()` methods from the `<ostream>` header file. The `put()` method outputs individual characters, and `write()` outputs a specified number of characters. The following code snippet demonstrates these methods briefly: