The ToUpper method returns a version of the string with all the letters converted to UPPER CASE. No other characters in the string are changed. There is a corresponding ToLower method as well.

# 4.11.7 Trimming and empty strings

Another useful method is Trim. This removes any leading or trailing spaces from the string.

```
s1=s1.Trim();
```

This is useful if your users might have typed " Rob " rather than "Rob". If you don't trim the text you will find equals tests for the name will fail. There are TrimStart and TrimEnd methods to just take off leading or trailing spaces if that is what you want. If you trim a string which contains only spaces you will end up with a string which contains no characters (i.e. its length is zero).

# 4.11.8 Character Commands

The char class also exposes some very useful methods which can be used to check the values of individual characters. These are static methods which can be called on the character class and can be used to test characters in a variety of ways.

| Method | Description |
|---|---|
| char.IsDigit(ch) | returns true if the character is a digit (0 to 9) |
| char.IsLetter(ch) | returns true if the character is a letter (a to z A to Z) |
| char.IsLetterOrDigit(ch) | returns true if the character is a letter or a digit |
| char.IsLower(ch) | returns true if the character is a lower case letter |
| char.IsUpper(ch) | returns true if the character is an upper case letter |
| char.IsPunctuation(ch) | returns true if the character is a punctuation character |
| char.IsWhiteSpace(ch) | returns true if the character is a space, tab or newline |

You can use these when you are looking through a string for a particular character.

# 4.11.9 String Twiddling with StringBuilder

If you really want to twiddle with the contents of your strings you will find the fact that you can't assign to individual characters in the string a real pain. The reason you are suffering is that strings are really designed to hold strings, not provide a way that they can be edited. For proper string editing C# provides a class called StringBuilder. It is found in the System.Text namespace.

It works a lot like a string, but you can assign to characters and even replace one string with another. It is also very easy to convert between StringBuilder instances and strings. You should look this up if you have a need to do some proper editing.

# 4.12 Properties

Properties are useful. They are a bit like the switch keyword, which lets us select things easily. We don't need properties, but C# provides them because they make programs slightly easier to write and simpler to read.