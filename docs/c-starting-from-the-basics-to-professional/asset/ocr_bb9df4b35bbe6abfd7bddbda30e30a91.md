You would more typically use `erase(s)` to remove a specific substring that you had previously searched for, so a more usual example might be as follows:

```
std::string word {"rose"};
size_t index {text.find(word)};
if (index != std::string::npos)
    text.erase(index, word.length());  // Second argument is a length, not an index!
```

This searches for word in text and, after confirming that it exists, removes it using `erase()`. The number of characters in the substring to be removed is obtained by calling the `length()` function for word. The `erase()` function can also be used with either one or no arguments; here’s an example:

```
text.erase(5);        // Removes all but the first 5 characters
text.erase();         // Removes all characters
```

After this last statement executes, text will be an empty string. Another function that removes all characters from a string object is `clear()`:

```
text.clear();
```

> **Caution**  Yet another common mistake is to call `erase(i)` with a single argument `i` in an attempt to remove a single character at the given index `i`. The actual effect of `erase(i)`, however, is quite different. It removes all characters starting from the one at index `i` all the way until the end of the string! To remove a single character at index `i`, you should use `erase(i,1)` instead.

With C++20 you can easily remove all occurrences of a given character using the nonmember `std::erase()` function. In this example, it is shown gutting a phrase from our favorite autogram-like movie quote:

```
std::string s { "The only verdict is vengeance; a vendetta, held as a votive not in vain."};
std::erase(s, 'v');
std::cout << s;  // The only erdict is eengeance; a endetta, held as a otive not in ain.
```

# std::string vs. std::vector<char>

You may have already noticed that `std::string` is similar to `std::vector<char>`. Both are dynamic arrays of char elements, complete with a `[]` operator to emulate plain char[] arrays. But the similarity goes well beyond that. A `std::string` object supports nearly all member functions that a `std::vector<char>` does. Evidently, this includes vector's functions you already know from Chapter 5:

+   - A string has a `push_back()` function to insert a new character at the end of the string (right before the termination character). It's not used that often, though, as `std::string` objects perform the more convenient `+=` syntax to append characters.
+   - A string has an `at()` function that, unlike the `[]` operator, performs bounds checking for the given index.