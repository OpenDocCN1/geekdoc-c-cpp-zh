If you want to enumerate all matches in a string, it is recommended to use the iterator variants over a loop with regex_match. There are cases where you might otherwise produce an infinite loop; regex_iterator prevents this. Therefore, especially with regular expressions that could match the "empty string," as "(abc)*", it is better to use the iterator variant.

# 28.2.6 Matches can do more than just output the found string with str(), as shown in Listing 28.10.

You can use length() and position() to find out exactly where the match occurs in the text. The text before and after the match is provided by the call prefix().str() and suffix().str(). Subexpressions, as you have already seen in Listing 28.12, can be obtained using operator[].

# 28.2.7 Options Regular expressions exist in the many different variants. If you do not specify otherwise, C++ supports the ECMAScript syntax—which is also known from JavaScript and is fundamentally related to Perl regular expression syntax. Anyone familiar with either should quickly find their way around in C++ as well. Other variants can be optionally supported by the implementation and are then selected via the constructor call:

```
regex rgx(R"...", regex_constants::Syntax);
```

Here, Syntax is a bitmask to select some different syntax variants. The standard specifies at least ECMAScript,