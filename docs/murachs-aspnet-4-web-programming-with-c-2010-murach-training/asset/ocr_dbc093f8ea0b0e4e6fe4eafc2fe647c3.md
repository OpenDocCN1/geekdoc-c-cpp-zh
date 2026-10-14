# How to create your own regular expressions

Figure 7-10 presents the basic elements of regular expressions. Although the .NET Framework provides many other elements that you can use in regular expressions, you can create expressions of considerable complexity using just the ones shown here. In fact, all of the standard expressions provided by ASP.NET use only these elements.

To start, you can specify any ordinary character, such as a letter or a decimal digit. If a character must be an A, for example, you just include that character in the expression. To include a character other than an ordinary character, you must precede it with a backslash. For example, \( specifies that the character must be a left parenthesis, \] specifies that the character must be a right bracket, and \\ specifies that the character must be a backslash. A backslash that’s used in this way is called an *escape character*.

You can also specify a *character class*, which consists of a set of characters. For example, \d indicates that the character must be a decimal digit, \w indicates that the character must be a *word character*, and \s indicates that the character must be a *whitespace character*. The uppercase versions of these elements—\D, \W, and \S—match any character that is not a decimal digit, word character, or whitespace character.

To create a list of possible characters, you enclose them in brackets. For example, [abc] specifies that the character must be the letter a, b, or c, and [a-z] specifies that the character must be a lowercase letter. One fairly common construct is [a-zA-Z], which specifies that the character must be a lowercase or uppercase letter.

You can also use *quantifiers* to indicate how many of the preceding element the input data must contain. To specify an exact number, you just code it in brackets. For example, \d{5} specifies that the input data must be a five-digit number. You can also specify a minimum number and a maximum number of characters. For example, \w{6,20} specifies that the input data must contain from six to twenty word characters. You can also omit the maximum number to require just a minimum number of characters. For example, \w{6,} specifies that the input data must contain at least 6 word characters. You can also use the *, ?, and + quantifiers to specify zero or more, zero or one, or one or more characters.

If the input data can match one or more patterns, you can use the vertical bar to separate elements. For example, \w+|s{1} means that the input data must contain one or more word characters or a single whitespace character.

To create groups of elements, you use parentheses. Then, you can apply quantifiers to the entire group or you can separate groups with a vertical bar. For example, (AB)|(SB) specifies that the input characters must be either AB or SB. And (\d{3}-)? specifies that the input characters must contain zero or one occurrence of a three-digit number followed by a hyphen.

To help you understand how you can use each of these elements, this figure presents several examples. If you study them, you’ll see the complex patterns that you can provide using these basic elements.