```
fragment Regular_String_Literal_Character
: Single_Regular_String_Literal_Character
| Simple_Escape_Sequence
| Hexadecimal_Escape_Sequence
| Unicode_Escape_Sequence
;

fragment Single_Regular_String_Literal_Character
: ~["\\u000D\u000A\u0085\u2028\u2029]   // anything but ", \, and
New_Line_Character
;

fragment Verbatim_String_Literal
: @' Verbatim_String_Literal_Character* ' '
;

fragment Verbatim_String_Literal_Character
: Single_Verbatim_String_Literal_Character
| Quote_Escape_Sequence
;

fragment Single_Verbatim_String_Literal_Character
: ~["']   // anything but quotation mark (U+0022)
;

fragment Quote_Escape_Sequence
: '""'
;
```

# Example: The example

```
string a = "Happy birthday, Joel"; // Happy birthday, Joel
string b = @"Happy birthday, Joel"; // Happy birthday, Joel
string c = "hello \t world"; // hello world
string d = @"hello \t world"; // hello \t world
string e = "Joe said \"Hello\" to me"; // Joe said "Hello" to me
string f = @"Joe said ""Hello"" to me"; // Joe said "Hello" to me
string g = "\\\\server\\share\\file.txt"; // \\server\share\file.txt
string h = @"\\server\share\file.txt"; // \\server\share\file.txt
string i = "one\r\ntwo\r\nthree";
string j = @"one
two
three";
```

shows a variety of string literals. The last string literal, j, is a verbatim string literal that spans multiple lines. The characters between the quotation marks, including white space such as new line characters, are preserved verbatim, and each pair of double-quote characters is replaced by one such character.

end example

Note: Any line breaks within verbatim string literals are part of the resulting string. If the exact characters used to form line breaks are semantically relevant to an application, any tools that translate line breaks in source code to different formats (between "\n" and "\r\n", for example) will change application behavior. Developers should be careful in such situations. end note