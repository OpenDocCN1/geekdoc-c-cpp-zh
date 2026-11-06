the first stream extraction reads `100` into the `int` variable `account` and
the second reads only `"Janie` into the `string` variable `name` (the
opening double quote would be part of the `string` in `name`). The third
stream extraction fails while attempting to read a value for the `double`
variable `balance`, because the next token (i.e., piece of data) in the
input stream—`Jones"`—is not a `double`.

# ## Reading Quoted Text

C++14’s new stream manipulator—`quoted` (header `<iomanip>`)—enables a program to read quoted text from a stream, *including* any white space characters in the quoted text, and discards the double quote delimiters. For example, if we read the preceding data using the expression

```
```cpp
inClientFile >> account >> quoted(name) >> balance
```
```

the first stream extraction reads `100` into `account`, the second reads `Janie Jones` as one `string` and stores it in `name` without the double-quote delimiters, and the third stream extraction reads `24.98` into `balance`. If the quoted data contains `\"` escape sequences, each is read and stored in the `string` as the escape sequence `\"`—not as `"`.