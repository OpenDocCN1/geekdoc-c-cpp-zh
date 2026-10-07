# More Fundamental Types 73

Also, with multiline string literals, there can be no characters following the initial set of double quotes or text prior to the closing of double quotes. Anything other than white space following the $$$" opening sequence or prior to the closing "" will result in a compile error.

By using a multiline string literal, you can avoid the problematic final quote within your text as shown in the example of mamaSaid variable in Listing 2.21.

# LISTING 2.21: Displaying Möbius Strip Using Raw String Literal

```
string firstName = "Forest";

// Single-line string literal.
string lastName = """Gump""";

// Single-line string literal with interpolation.
string greeting = $\$\"Hello, {firstName}{lastName}";"

string proposal = "Do you want a chocolate?"
  * "I could eat about a million and a half of these."

string mamaSaid = // Multiline-raw string literal
"""
  Mama said, "Life was just a box of chocolates..."
  """

string jsonDialogue = 

// Multiline-raw string literal with interpolation.
{
  "quote": {
    "character": "The MAN",
    "dialogue": "{{greeting}}"
  },
  "description": "She nods, not much interested. He...",
  "quote": {
    "character": "The MAN",
    "dialogue": "{{proposal}}"
  },
  "description": "She shakes \nno" He unraps it...",
  "quote": {
    "character": "The MAN",
    "dialogue": "{{mamaSaid.Replace(\"\", \\\\"")}}"
  }
}
```