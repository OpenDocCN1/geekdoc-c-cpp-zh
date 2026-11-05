includes a delimited comment.

end example

A single-line comment begins with the characters // and extends to the end of the line.

Example: The example

```
// Hello, world program
// This program writes "hello, world" to the console
//
class Hello // any name will do for this class
{
    static void Main() // this method must be named "Main"
    {
        System.Console.WriteLine("hello, world");
    }
}
```

shows several single-line comments.

end example

```
Comment
  : Single_Line_Comment
  | Delimited_Comment
  ;

fragment Single_Line_Comment
  : '//' Input_Character*
  ;

fragment Input_Character
  // anything but New_Line_Character
  : ~('\u000D' | '\u000A' | '\u0085' | '\u2028' | '\u2029')
  ;

fragment New_Line_Character
  : '\u000D' // carriage return
  | '\u000A' // line feed
  | '\u0085' // next line
  | '\u2028' // line separator
  | '\u2029' // paragraph separator
  ;

fragment Delimited_Comment
  : '/*' Delimited_Comment_Section* ASTERISK+ '/'
  ;

fragment Delimited_Comment_Section
  : SLASH
  | ASTERISK* Not_Slash_Or_Asterisk
  ;

fragment Not_Slash_Or_Asterisk
  : ~('/' | '*')  // Any except SLASH or ASTERISK
  ;
```