# LISTING 2.18: Single Line Raw String Literal⁵

```
Console.WriteLine(
  ""Mama said, "Life was just a box of chocolates..." """);
```

we can't end the string with double quotes when it begins with three. The ending quote count must match the begin quote count, and if they don't match, the compiler issues an error. (The solution to avoiding the extra space is provided by multiline raw string literals in the section.)

The reason that raw string literals allow for more than three double quotes to delineate the raw string literal is to allow placement of three (or more) consecutive double quotes within the text. With five double quotes at the start and end of the raw string literal, for example, you can place four consecutive double quotes within the text and have them interpreted literally as four consecutive double quotes.

You also can include interpolation in Listing 2.19 with raw string literals.

# LISTING 2.19: Raw String Literals with Interpolation

```
Console.WriteLine(
  """Hello, I'm {firstName}. {lastName}"""");
```

However, an additional complexity is that the curly brace into which you place the expression must match the number of dollar symbols ($) you place at the beginning of the string. For example, two dollar symbols would require each expression to be surrounded by two curly braces. Listing 2.20 provides an example of that curly braces surround mobius (Two dollar symbols require two curly braces to render the name expression, resulting in a curly brace pair in the output because there are three curly brace pairs used in the code).

Additionally, Listing 2.20 demonstrates a multiline version of raw string literals (multiline string literals).

# LISTING 2.20: Displaying Mobius Strip Using Raw String Literal

```
string name = "mobius";
Console.Write(
  $$"""");
```

> 5. Refer to the movie Forrest Gump if you're confused about the dialogue found in this section.