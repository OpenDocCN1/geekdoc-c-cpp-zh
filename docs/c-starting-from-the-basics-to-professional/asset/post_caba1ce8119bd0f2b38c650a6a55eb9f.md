
This loop applies the `toupper()` function to each character in the string in turn and stores the result in the same position in the string. You best add a `static_cast<char>` to silence compiler warnings for implicit narrowing (the C function `toupper()` returns a value of type `int`, and not of type `char` as desired). The index value for the first character is 0, and the index value for the last character is one less than the length of the string, so the loop continues as long as `i < sentence.length()` is true.

A string object is a range, so you could also do this with a range-based `for` loop:

```cpp
for (char& ch : sentence)
    ch = static_cast<char>(std::toupper(ch));
```

Specifying `ch` as a reference type allows the character in the string to be modified within the loop. This loop and the previous loop require the `<cctype>` C header to be included to compile.

You can exercise this array-style access method in a version of `Ex5_10.cpp` that determined the number of vowels and consonants in a string. The new version will use a string object. It will also demonstrate that you can use the `getline()` function to read a line of text that includes spaces:

```cpp
// Ex7_02.cpp
// Accessing characters in a string
import <iostream>;
import <string>;
#include <cctype>

int main()
{
    std::string text;                      // Stores the input
    std::cout << "Enter a line of text:\n";
    std::getline(std::cin, text);          // Read a line including spaces

    unsigned vowels {};                    // Count of vowels
    unsigned consonants {};                // Count of consonants
    for (size_t i {}; i < text.length(); ++i)
    {
        if (std::isalpha(text[i]))         // Check for a letter
        {
            switch (std::tolower(text[i])) // Convert to lowercase
            {
                case 'a': case 'e': case 'i': case 'o': case 'u':
                    ++vowels;
                    break;

                default:
                    ++consonants;
                    break;
            }
        }
    }

    std::cout << "Your input contained " << vowels << " vowels and "
              << consonants << " consonants." << std::endl;
}
```

Here's an example of the output:

```text
Enter a line of text:
A nod is as good as a wink to a blind horse.
Your input contained 14 vowels and 18 consonants.
```

The text object contains an empty string initially. You read a line from the keyboard into text using the `getline()` function. This version of `getline()` is declared in the `<string>` module; the versions of `getline()` that you have used previously were declared in the `<iostream>` module. This version reads characters from the stream specified by the first argument, `cin` in this case, until a newline character is read, and the result is stored in the string object specified by the second argument, which is `text` in this case. This time you don't need to worry about how many characters are in the input. The string object will automatically accommodate however many characters are entered, and the length will be recorded in the object.

You can change the delimiter that signals the end of the input by using a version of `getline()` with a third argument that specifies the new delimiter for the end of the input:

```cpp
std::getline(std::cin, text, '#');
```

This reads characters until a `'#'` character is read. Because a newline doesn't signal the end of input in this case, you can enter as many lines of text as you like, and they'll all be combined into a single string. Any newline characters that were entered will be present in the string.

You count the vowels and consonants in much the same way as in Ex5_10.cpp, using a for loop. Naturally, you could also use range-based for loop instead:

```cpp
for (const char ch : text)
{
    if (std::isalpha(ch))          // Check for a letter
    {
        switch (std::tolower(ch))  // Convert to lowercase
        {
            ...
        }
    }
}
```

This code, available in Ex7_02A.cpp, is simpler and easier to understand than the original. The major advantage of using a string object in this example compared to Ex5_10.cpp, though, remains the fact that you don't need to worry about the length of the string that is entered.

## Accessing Substrings

You can extract a substring from a string object using its `substr()` function. The function requires two arguments. The first is the index position where the substring starts, and the second is the number of characters in the substring. The function returns the substring as a string object. Here's an example:

```cpp
std::string phrase {"The higher the fewer."};
std::string word1 {phrase.substr(4, 6)};   // "higher"
```

This extracts the six-character substring from phrase that starts at index position 4, so word1 will contain "higher" after the second statement executes. If the length you specify for the substring overruns the end of the string object, then the `substr()` function just returns an object containing the characters up to the end of the string. The following statement demonstrates this behavior:

```cpp
std::string word2 {phrase.substr(4, 100)};  // "higher the fewer."
```

Of course, there aren’t 100 characters in phrase, let alone in a substring. In this case, the result will be that word2 will contain the substring from index position 4 to the end, which is "higher the fewer.". You could obtain the same result by omitting the length argument and just supplying the first argument that specifies the index of the first character of the substring:

```cpp
std::string word {phrase.substr(4)};        // "higher the fewer."
```

This version of `substr()` also returns the substring from index position 4 to the end. If you omit both arguments to `substr()`, the whole of phrase will be selected as the substring.

If you specify a starting index for a substring that is outside the valid range for the string object, an exception of type `std::out_of_range` will be thrown, and your program will terminate abnormally—unless you’ve implemented some code to handle the exception. You don’t know how to do that yet, but we’ll discuss exceptions and how to handle them in Chapter 16.

> **Caution**
> 
> As before, substrings are always specified using their beginning index and length, not using their beginning and ending indexes. Keep this in mind when migrating from languages such as JavaScript or Java!

## Comparing Strings

In example Ex7_02 you used an index to access individual characters in a string object for comparison purposes. When you access a character using an index, the result is of type `char`, so you can use the comparison operators to compare individual characters. You can also compare entire string objects using any of the comparison operators. These are the comparison operators you can use:

```text
>    >=    <    <=    ==    !=    <=>
```

You can use these to compare two objects of type string or to compare a string object with a string literal or C-style string. When comparing string objects, the `<=>` operator results in a `std::strong_ordering` (see Chapter 4)—but much more on that in the next subsection.

For all seven operators, the operands are compared character by character until either a pair of corresponding characters contains different characters or the end of either or both operands is reached. When a pair of characters differs, numerical comparison of the character codes determines which of the strings has the lesser value. If no differing character pairs are found and the strings are of different lengths, the shorter string is "less than" the longer string. Two strings are equal if they contain the same number of characters and all corresponding character codes are equal. Because you’re comparing character codes, the comparisons are obviously going to be case sensitive.

The technical term for this string comparison algorithm is *lexicographical comparison*, which is just a fancy way of saying that strings are ordered in the same manner as they are in a dictionary or phone book¹. You could compare two string objects using this if statement:

```cpp
std::string word1 {"age"};
std::string word2 {"beauty"};
if (word1 < word2)
    std::cout << word1 << " comes before " << word2 << '.' << std::endl;
else
    std::cout << word2 << " comes before " << word1 << '.' << std::endl;
```

Executing these statements will result in the following output:

```text
age comes before beauty.
```

This shows that the old saying must be true. The preceding code looks like a good candidate for using the conditional operator. You can produce a similar result with the following statement:

```cpp
std::cout << word1 << (word1 < word2 ? " comes " : " does not come ")
          << "before " << word2 << '.' << std::endl;
```

Let’s compare strings in a working example. This program reads any number of names and sorts them into ascending sequence:

```cpp
// Ex7_03.cpp
// Comparing strings
import <iostream>;      // For stream I/O
import <format>;        // For string formatting
import <string>;        // For the string type
import <vector>;        // For the vector container

int main()
{
    std::vector<std::string> names;    // Vector of names
    std::string input_name;            // Stores a name

    for (;;)                           // Indefinite loop (stopped using break)
    {
        std::cout << "Enter a name followed by Enter (leave blank to stop): ";
        std::getline(std::cin, input_name);  // Read a name and...
        if (input_name.empty()) break;       // ...if it's not empty...
        names.push_back(input_name);         // ...add it to the vector
    }
}
```

¹Or, for our younger readers who are no longer familiar with archaic paper relics such as dictionaries and phone books: in the same manner as your contacts are ordered on your smart phone.
