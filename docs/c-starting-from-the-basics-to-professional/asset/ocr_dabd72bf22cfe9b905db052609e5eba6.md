# Using `rfind()` with one argument

```
```cpp
string sentence {"Manners maketh man"};
string word {"an"};
```
```

![](bbox=[0.169, 0.242, 0.782, 0.423])

**As with find(), if the argument is not found, then the value `string::npos` is returned.**

Searching with word as the argument finds the last occurrence of "an" in the string. The `rfind()` function returns the index position of the first character in the substring sought.

If the substring isn't present, no position will be returned. For example, the following statement will result in this:

```
```cpp
std::cout << sentence.rfind("miners") << std::endl;  // Outputs std::string::npos
```
```

The sentence doesn't contain the substring "miners", so `npos` will be returned and displayed by this statement. The other two searches illustrated in Figure 7-4 are similar to the first. They both search backward from the end of the string looking for the first occurrence of the argument.

Just as with `find()`, you can supply an extra argument to `rfind()` to specify the starting index for the backward search, and you can add a third argument when the first argument is a C-style string. The third argument specifies the number of characters from the C-style string that are to be taken as the substring for which you're searching.

# Modifying a String

Once you've searched a string and found what you're looking for, you may well want to change the string in some way. You've already seen how you can use an index between square brackets to select a single character in a string object. You can also insert a string into a string object at a given index or replace a substring. Unsurprisingly, to insert a string, you use a function called `insert()`, and to replace a substring in a string, you use a function called `replace()`. We'll explain inserting a string first.