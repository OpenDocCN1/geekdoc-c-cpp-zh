This reads characters up to the first whitespace character, which ends the input process. Whatever was read is stored in the string object, `name`. You cannot enter text with embedded spaces with this process. Of course, reading entire phrases complete with spaces is possible as well, just not with `>>`. We'll explain how you do this later.

To summarize, in this section we have described six options for defining and initializing a string object; the following comments identify the initializing string in each case:

+   1. No initializer (or empty braces, `{}`):
+   
+   ```cpp
+   std::string empty;                 // The string ""
+   ```

+   2. An initializer containing a string literal:
+   
+   ```cpp
+   std::string proverb{ "Many a mickle makes a muckle." };   // The given literal
+   ```

+   3. An initializer containing an existing string object:
+   
+   ```cpp
+   std::string sentence{ proverb };    // Duplicates proverb
+   ```

+   4. An initializer containing a string literal followed by the length of the sequence in the literal to be used to initialize the string object:
+   
+   ```cpp
+   std::string part_literal{ "Least said soonest mended.", 5 };   // "Least"
+   ```

+   5. An initializer containing a repeat count followed by the character literal that is to be repeated in the string that initializes the string object (mind the round parentheses!):
+   
+   ```cpp
+   std::string open_wide(5, 'a');       // "aaaaa"
+   ```

+   6. An initializer containing an existing string object, an index specifying the start of the substring, and the length of the substring:
+   
+   ```cpp
+   std::string phrase{proverb, 5, 8};   // "a mickle"
+   ```

A seventh option (see a Standard Library reference for the full list) is to create a string from an existing `std::string` object and only a single integer number. The resulting string object then contains a substring starting at the given index. Here is an example:

```
```cpp
std::string string{ "Consistency is the key to success" };
std::string part_string{ string, 15 };   // "the key to success"
```
```