# 31.2 Example Usage

Two overloaded functions are provided:

+   - std::from_chars() converts a given character sequence into a numeric value.
+   - std::to_chars() converts numeric values into a given character sequence.

# 31.2.1 from_chars()

std::from_chars() converts a given character sequence into a numeric value. For example:

```
#include <charconv>
```

```
const char* str = "12 monkeys";
int value;
std::from_chars_result res = std::from_chars(str, str+10,
    value);
```

After a successful parsing, value contains the parsed value (12 in this example). The result value is the following structure:

```
struct from_chars_result {
    const char* ptr;
    std::errc ec;
};
```

After the call, ptr refers to the first character not parsed as part of the number (or the passed second argument, if all characters were parsed) and ec contains an error condition of type std::errc or is equal to std::errc{} if the conversion was successful. Thus, you can check the result as follows:

```
if (res.ec != std::errc{}) {
    ...  // error handling
}
```

Note that there is no implicit conversion to bool for std::errc, which means that you cannot check the value as follows:

```
if (res.ec) {  // ERROR: no implicit conversion to bool
```

or:

```
if (!res.ec) { // ERROR: no operator! defined
```

However, by using structured bindings and if with initialization, you can write:

```
if (auto [ptr, ec] = std::from_chars(str, str+10, value); ec != std::errc{}) {
    ...  // error handling
}
```