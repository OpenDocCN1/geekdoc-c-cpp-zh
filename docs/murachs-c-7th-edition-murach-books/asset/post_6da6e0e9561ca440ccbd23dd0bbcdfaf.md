
## How to work with strings

Many types of programs require that you work with the characters within strings. If, for example, a user enters the city, state, and zip code of an address as a single entry, your program may need to divide (or parse) that single string into city, state, and zip code variables. Or, if a user enters a telephone number that includes parentheses and hyphens, you may need to remove those characters so the number can be stored as a 10-digit integer.

When you create a string, you are actually creating a String object from the String class. Then, you can use the properties and methods of the String class to work with the String object. Another alternative, though, is to create StringBuilder objects from the StringBuilder class so you can use the properties and methods of that class to work with strings. In the topics that follow, you’ll learn both ways of working with strings.

### The properties and methods of the String class

Figure 9-5 summarizes some of the properties and methods of the String class that you can use as you work with String objects. When you use these properties and methods, you often need to use an index to refer to a specific character within a string. To do that, you use 0 to refer to the first character, 1 to refer to the second character, and so on. When you refer to a character in a string, you code the index for a string character within brackets. This is the same technique that you use to refer to an element of an array. In fact, it sometimes helps to think of a string as an array of characters.

One method that’s particularly useful for parsing strings is Split(). This method returns an array where each element contains a substring of the original string. The argument that you specify for this method identifies the character that’s used to delimit each substring. You’ll see examples of this method in figure 9-7.

### Common properties and methods of the String class

| Type | Member | Description |
| --- | --- | --- |
| Indexer | `[index]` | Gets the character at the specified position. |
| Property | `Length` | Gets the number of characters in the string. |
| Method | `StartsWith(string)` | Returns a Boolean value that indicates whether or not the string starts with the specified string. |
| Method | `EndsWith(string)` | Returns a Boolean value that indicates whether or not the string ends with the specified string. |
| Method | `IndexOf(string[, startIndex])` | Returns an integer that represents the position of the first occurrence of the specified string starting at the specified position. If the starting position isn’t specified, the search starts at the beginning of the string. If the string isn’t found, -1 is returned. |
| Method | `LastIndexOf(string[, startIndex])` | Returns an integer that represents the position of the last occurrence of the specified string starting at the specified position. If the starting position isn’t specified, the search starts at the end of the string. If the string isn’t found, -1 is returned. |
| Method | `Insert(startIndex, string)` | Returns a string with the specified string inserted beginning at the specified position. |
| Method | `PadLeft(totalWidth)` | Returns a string that’s right-aligned and padded on the left with spaces so it’s the specified width. |
| Method | `PadRight(totalWidth)` | Returns a string that’s left-aligned and padded on the right with spaces so it’s the specified width. |
| Method | `Remove(startIndex, count)` | Returns a string with the specified number of characters removed starting at the specified position. |
| Method | `Replace(oldString, newString)` | Returns a string with all occurrences of the old string replaced with the new string. |
| Method | `Substring(startIndex[, length])` | Returns the string that starts at the specified position and has the specified length. If the length isn’t specified, all of the characters to the end of the string are returned. |
| Method | `ToLower()` | Returns a string in lowercase. |
| Method | `ToUpper()` | Returns a string in uppercase. |
| Method | `Trim()` | Returns a string with leading and trailing spaces removed. |
| Method | `Split(splitCharacters)` | Returns an array of strings where each element is a substring that’s delimited by the specified character or characters. |

- You can use an index to access each character in a string, where 0 is the index for the first character, 1 is the index for the second character, and so on.

Figure 9-5 The properties and methods of the String class

### Code examples that work with strings

Figure 9-6 shows how to use most of the properties and methods summarized in the last figure. The first example shows how you can use an index to return a character from a string. Then, the second example shows how you can use an index and the Length property in a for loop to insert a space character between each character in the string. The third example performs the same operation as the second example, but it uses a foreach loop instead of a for loop.

The fourth example shows how you can use the StartsWith() and EndsWith() methods. Here, the first statement checks if the string named chars that was created in the first example starts with the string “abc”, and the second statement checks if this string ends with “abc”. As you can see, the result of the first statement is true, and the result of the second statement is false.

The fifth example shows how to use the IndexOf() and LastIndexOf() methods. Here, the first statement sets the value of the string. Then, the second and third statements use the IndexOf() method to retrieve the index of the first space in the string. The fourth statement uses the same method to return the index of a string of characters. Since the characters don’t exist in the string, this method returns a value of -1. The last statement uses the LastIndexOf() method to return the index of the last space in the string.

The sixth example shows how to use the Remove(), Insert(), and Replace() methods to work with the string in the fifth example. Here, the first statement removes the first five characters of the string. In this statement, the first argument specifies the starting index, and the second argument specifies the number of characters to remove. In this case, the number of characters to remove is calculated by adding 1 to the index of the first space, which is 4. Then, the second statement uses the Insert() method to insert “, Inc.” at the end of the string. Here, the first argument uses the Length property to set the starting index at the end of the string, and the second argument specifies the string to be inserted. Finally, the third statement uses the Replace() method to replace all occurrences of “and” with “And”.

The seventh example shows how to use the Substring(), ToUpper(), and ToLower() methods to make sure a string is lowercase with an initial cap. Here, the second statement returns a substring that contains the first character in the string. To do that, the first argument specifies a starting index of 0 and the second argument specifies a length of 1. Then, to convert the returned substring to uppercase, this statement calls the ToUpper() method. The third statement is similar, but it uses the ToLower() method to return the remaining characters in the string and convert them to lowercase. The last statement combines the two strings into a single string.

The eighth example shows how to use the = operator to copy one string to another string. Because a string is a reference type, you might think that the second statement would copy the reference to the string object created by the first statement to the second string variable. In this case, however, a new string object is created and the value in the original string is copied to that object. Then, a reference to the new object is assigned to the new string variable.

### Code that uses an index to access a character in a string

```
string chars = "abcdefg";
char a = chars[0];                 // 'a'
char b = chars[1];                 // 'b'
```

### Code that uses a for loop to access each character in the string

```
string charsAndSpaces = "";
for (int i = 0; i < chars.Length; i++)
    charsAndSpaces += chars[i] + " ";
MessageBox.Show(charsAndSpaces, "String Test");
```

### The message box that's displayed

![](img/844f608d10a44654833ea5efc8a2e7a7_304_0.png)

### Code that uses a foreach loop to access each character in the string

```
string charsAndSpaces = "";
foreach (char c in chars)
    charsAndSpaces += c + " ";
MessageBox.Show(charsAndSpaces, "String Test");
```

### Code that uses the StartsWith() and EndsWith() methods

```
bool startsWithABC = chars.StartsWith("abc");   // true
bool endsWithABC = chars.EndsWith("abc");       // false
```

### Code that uses the IndexOf() and LastIndexOf() methods

```
string companyName = "Mike Murach and Associates";
int index1 = companyName.IndexOf(" ");        // 4
int index2 = companyName.IndexOf(' ');          // 4
int index3 = companyName.IndexOf("Inc.");      // -1
int index4 = companyName.LastIndexOf(" ");     // 15
```

### Code that uses the Remove(), Insert(), and Replace() methods

```
companyName = companyName.Remove(0, index1 + 1);
companyName = companyName.Insert(companyName.Length, ", Inc.");
companyName
    = companyName.Replace("and", "And");          // Murach And Associates, Inc.
```

### Code that uses the Substring(), ToUpper(), and ToLower() methods

```
string firstName = "anne";
string firstLetter = firstName.Substring(0, 1).ToUpper();
string otherLetters = firstName.Substring(1).ToLower();
firstName = firstLetter + otherLetters;          // Anne
```

### Code that copies one string to another string

```
string s1 = "abc";
string s2 = s1;      // this copies the value stored in s1 to s2
s2 = "def";        // this doesn't change the value stored in s1
```
