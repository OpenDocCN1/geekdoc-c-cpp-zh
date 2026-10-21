# Joining Strings

You can use the + operator to join strings to form a new String object. Here’s an example:

```
String^ name1 = L"Beth";
String^ name2 = L"Betty";
String^ name3 = name1 + L" and " + name2;
```

After executing these statements, name3 contains the string "Beth and Betty". Note how you can use the + operator to join String objects with string literals. You can also join String objects with numerical values or bool values and have the values converted automatically to a string before the join operation. The following statements illustrate this:

```
String^ str = L"Value: ";
String^ str1 = str + 2.5;            // Result is new string "Value: 2.5"
String^ str2 = str + 25;            // Result is new string "Value: 25"
String^ str3 = str + true;          // Result is new string "Value: True"
```

You can also join a String and a character, but the result depends on the type of character:

```
char ch = 'Z';
wchar_t wch = 'Z'
String^ str4 = str + ch;            // Result is new string "Value: 90"
String^ str5 = str + wch;           // Result is new string "Value: Z"
```

The comments show the results of the operations. A character of type char is treated as a numerical value so you get the character code value joined to the string. The wchar_t character is of the same type as the characters in the String object (type Char) so the character is appended to the string.

Don’t forget that String objects are immutable; once created, they cannot be changed. This means that all operations that apparently modify String objects always result in new String objects being created.

The String class also defines a Join() function that you use when you want to join a series of strings stored in an array into a single string with separators between the original strings. Here’s how you could join names together in a single string with the names separated by commas:

```
array<String^>^ names = { "Jill", "Ted", "Mary", "Eve", "Bill"};
String^ separator = ", ";
String^ joined = String::Join(separator, names);
```

After executing these statements, joined references the string "Jill, Ted, Mary, Eve, Bill". The separator string has been inserted between each of the original strings in the names array. Of course, the separator string can be anything you like(it could be " and ", for example, which results in the string "Jill and Ted and Mary and Eve and Bill".

Let’s try a full example of working with String objects.