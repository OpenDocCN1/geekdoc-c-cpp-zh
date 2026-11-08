
The replacement string can be a string object or a null-terminated string. In the former case, you can specify a start index and a length to select a substring as the replacement string. For example, the previous replace operation could have been this:

```cpp
std::string name { "Amos Gruntfuttock" };
text.replace(start, end - start, name, 5, 12);
```

These statements have the same effect as the previous use of replace() because the replacement string starts at position 5 of name (which is the 'G') and contains 12 characters.

If the first argument is a null-terminated string, you can specify the number of characters that are the replacement string. Here's an example:

```cpp
text.replace(start, end - start, "Gruntfuttock, Amos", 12);
```

This time, the string to be substituted consists of the first 12 characters of "Gruntfuttock, Amos," so the effect is the same as the previous replace operation.

A further possibility is to specify the replacement string as multiples of a given character. For example, you could replace "Jones" by three asterisks with this statement:

```cpp
text.replace(start, end - start, 3, '*');
```

This assumes that start and end are determined as before. The result is that text will contain the following:

```text
Smith, where *** had had "had had", had had "had".
```

Let's try the replace operation in an example. This program replaces all occurrences of a given word in a string with another word:

```cpp
// Ex7_07.cpp
// Replacing words in a string
import <iostream>;
import <string>;

int main()
{
    std::string text;                         // The string to be modified
    std::cout << "Enter a string terminated by *:\n";
    std::getline(std::cin, text, '*');

    std::string word;                         // The word to be replaced
    std::cout << "Enter the word to be replaced: ";
    std::cin >> word;

    std::string replacement;                  // The word to be substituted
    std::cout << "Enter the string to be substituted for " << word << ": ";
    std::cin >> replacement;

    if (word == replacement)                       // Verify there's something to do
    {
        std::cout << "The word and its replacement are the same.\n"
                  << "Operation aborted." << std::endl;
        return 1;
    }

    size_t start {text.find(word)};                 // Index of 1st occurrence of word
    while (start != std::string::npos)              // Find and replace all occurrences
    {
        text.replace(start, word.length(), replacement); // Replace word
        start = text.find(word, start + replacement.length());
    }

    std::cout << "\nThe string you entered is now:\n" << text << std::endl;
}
```

Here's a sample of the output:

```text
Enter a string terminated by *:
A rose is a rose is a rose.*
Enter the word to be replaced: rose
Enter the string to be substituted for rose: dandelion

The string you entered is now:
A dandelion is a dandelion is a dandelion.
```

The string that is to have words replaced is read into text by getline(). Any number of lines can be entered and terminated by an asterisk. The word to be replaced and its replacement are read using the extraction operator and therefore cannot contain whitespace. The program ends immediately if the word to be replaced and its replacement are the same.

The index position of the first occurrence of word is used to initialize start. This is used in the while loop that finds and replaces successive occurrences of word. After each replacement, the index for the next occurrence of word in text is stored in start, ready for the next iteration. When there are no further occurrences of word in text, start will contain npos, which ends the loop. The modified string in text is then output.

## Removing Characters from a String

You could always remove a substring from a string object using the replace() function: you just specify the replacement as an empty string. But there's also a specific function for this purpose, erase(). You specify the substring to be erased by the index position of the first character and the length. For example, you could erase the first six characters from text like this:

```cpp
text.erase(0, 6);    // Remove the first 6 characters
```

You would more typically use `erase()` to remove a specific substring that you had previously searched for, so a more usual example might be as follows:

```cpp
std::string word {"rose"};
size_t index {text.find(word)};
if (index != std::string::npos)
    text.erase(index, word.length());  // Second argument is a length, not an index!
```

This searches for word in text and, after confirming that it exists, removes it using `erase()`. The number of characters in the substring to be removed is obtained by calling the `length()` function for word. The `erase()` function can also be used with either one or no arguments; here’s an example:

```cpp
text.erase(5);        // Removes all but the first 5 characters
text.erase();         // Removes all characters
```

After this last statement executes, text will be an empty string. Another function that removes all characters from a string object is `clear()`:

```cpp
text.clear();
```

> **Caution**  Yet another common mistake is to call `erase(i)` with a single argument `i` in an attempt to remove a single character at the given index `i`. The actual effect of `erase(i)`, however, is quite different. It removes all characters starting from the one at index `i` all the way until the end of the string! To remove a single character at index `i`, you should use `erase(i, 1)` instead.

With C++20 you can easily remove all occurrences of a given character using the nonmember `std::erase()` function. In this example, it is shown gutting a phrase from our favorite lipogram-like movie quote:

```cpp
std::string s { "The only verdict is vengeance; a vendetta, held as a votive not in vain." };
std::erase(s, 'v');
std::cout << s;  // The only erdict is engeance; a endetta, held as a otive not in ain.
```

## std::string vs. std::vector<char>

You may have already noticed that `std::string` is similar to `std::vector<char>`. Both are dynamic arrays of char elements, complete with a `[]` operator to emulate plain char[] arrays. But the similarity goes well beyond that. A `std::string` object supports nearly all member functions that a `std::vector<char>` does. Evidently, this includes vector's functions you already know from Chapter 5:

- A string has a `push_back()` function to insert a new character at the end of the string (right before the termination character). It's not used that often, though, as `std::string` objects perform the more convenient `+=` syntax to append characters.
- A string has an `at()` function that, unlike the `[]` operator, performs bounds checking for the given index.
- A string has a `size()` function, which is an alias for `length()`. The latter was added because it's more common to talk about the “length of a string” than the “size of a string.”
- A string offers `front()` and `back()` convenience functions to access its first and last characters (not counting the null termination character).
- A string supports a range of `assign()` functions to reinitialize it. These functions accept argument combinations similar to those you can use between the braced initializers when first initializing a string. So, assigning `("x", 5)` for instance, reinitializes `s` to `"xxx"`, and `s.assign("Reinitialize", 2, 4)` overwrites the contents of the string object `s` with `"init"`.

If this chapter has made one thing clear, though, then it's that a `std::string` is so much more than a simple `std::vector<char>`. On top of the functions provided by a `vector<char>`, it offers a wide range of additional, useful functions for common string manipulations such as concatenation, substring access, string searches and replacements, and so on. And of course, a `std::string` is aware of the null character that terminates its char array and knows to take this into account in members such as `size()`, `back()`, and `push_back()`.

## Converting Strings into Numbers

Earlier in this chapter you learned that you can use `std::to_string()` to convert numbers into strings. But what about the other direction: how do you convert strings such as `"123"` and `"3.1415"` into numbers? There are several ways to accomplish this in C++, but it's again the `<string>` module that provides you with the easiest option. Its `std::stoi()` function, short for “string to int,” converts a given string to an int:

```cpp
std::string s{ "123" };
int i{ std::stoi(s) };        // i == 123
```

The `<string>` module similarly offers `stol()`, `stoll()`, `stoul()`, `stoull()`, `stof()`, `stod()`, and `stold()`, all within the `std` namespace, to convert a string into a value of, respectively, type `long`, `long long`, `unsigned long`, `unsigned long long`, `float`, `double`, and `long double`.

## Strings of International Characters

You'll remember from Chapter 1 that, internationally, many more characters are in use than the 128 that are defined by the standard ASCII character set. French and Spanish, for instance, often use accented letters such as é, á, or ñ. Languages such as Russian, Arabic, Malaysian, or Japanese of course use characters that are completely different from those defined by the ASCII standard. The 256 different characters you could potentially represent with a single 8-bit char are not nearly enough to represent all these possible characters. The Chinese script alone consists of many tens of thousands of characters!

Supporting multiple national character sets is an advanced topic, so we'll only introduce the basic facilities that C++ offers, without going into detail of how you apply any of them. Thus, this section is just a pointer to where you should look when you have to work with different national character sets. Potentially, you have four options for working with strings that may contain extended character sets:

- You can define `std::wstring` objects that contain strings of characters of type `wchar_t`—the wide-character type that is built into your C++ implementation.
