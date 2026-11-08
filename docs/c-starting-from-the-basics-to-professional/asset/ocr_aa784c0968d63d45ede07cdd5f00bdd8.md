# Concatenating Strings and Numbers

An important limitation in C++ is that you can only concatenate `std::string` objects with either strings or characters. Concatenation with most other types, such as a double, will generally fail to compile:

```
const std::string result_string{ "The result equals: "};
double result = std::numbers::pi;
std::cout << (result_string + result) << std::endl;    // Compiler error!
```

Worse, such concatenations sometimes compile and produce undesired results, because numbers may again be treated as character codes. Here is an example (the ASCII code for the letter 'E' is 69):

```
std::string song_title { "Summer of " };
song_title += 69;
std::cout << song_title << std::endl;    // Summer of 'E
```

This limitation might frustrate you at first, especially if you’re used to working with strings in, for instance, Java or C#. In those languages, the compiler implicitly converts values of any type to strings. Not so in C++. In C++, you have to explicitly convert these values to strings yourself. There are several ways you might accomplish this. For values of fundamental numeric types, a quick and easy way is the `std::to_string()` family of functions defined in the `<string>` module:

```
const std::string result_string{ "The result equals: "};
double result = std::numbers::pi;
std::cout << (result_string + std::to_string(result)) << std::endl;    // 3.141593

std::string song_title { "Summer of " };
song_title += std::to_string(69);
std::cout << song_title << std::endl;    // Summer of '69
```

You cannot, however, control the format used by `std::to_string()`. For floating-point numbers, for instance, `std::to_string()` will always use fixed-point output with precision 6. If you want more control you can of course use `std::format()` instead (without string concatenation then typically):

```
std::cout << std::format("The result equals: {:.15f}\n", result);    // 3.141592653589793
std::cout << std::format("Summer of '{:x}\n", 105); // Summer of '69 (hexadecimal for 105)
```

# Accessing Characters in a String

You refer to a particular character in a string by using an index value between square brackets, just as you do with a character array. The first character in a string object has the index value 0. You could refer to the third character in sentence, for example, as sentence[2]. You can use such an expression on the left of the assignment operator, so you can replace individual characters as well as access them. The following loop changes all the characters in sentence to uppercase:

```
for (size_t i {}; i < sentence.length(); ++i)
    sentence[i] = static_cast<char>(std::toupper(sentence[i]));
```