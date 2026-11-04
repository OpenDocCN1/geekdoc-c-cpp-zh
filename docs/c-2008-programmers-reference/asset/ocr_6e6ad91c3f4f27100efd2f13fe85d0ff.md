# Part I: C# Fundamentals

Another common search pattern is verifying a string containing a date. For example, if a string contains a date in the format "yyyy/mm/dd", you would specify the search pattern as follows: "[19|20]\d\d[- /.]{0[1-9]|1[012]}[- /.]{0[1-9]|1[012]}". This pattern will match dates ranging from 1900-01-01 to 2099-12-31.

```
string date = "2007/03/10";
Regex r = new Regex(@"[19|20]\d\d[- /.]{0[1-9]|1[012]}[- /.]{0[1-9]|1[012]}");
if (r.IsMatch(date))
{
    Console.WriteLine("Matches.");
}
```

You can use the following date separators with the pattern specified above:

```
string date = "2007/03/10";
string date = "2007-03-10";
string date = "2007 03 10";
string date = "2007.03.10";
```

Some commonly used search patterns are described in the following table.

| Pattern | Description |
|---|---|
| [0-9] | Digits |
| [A-Fa-f0-9] | Hexadecimal digits |
| [A-Za-z0-9] | Alphanumeric characters |
| [A-Za-z] | Alphabetic characters |
| [a-z] | Lowercase letters |
| [A-Z] | Uppercase letters |
| [ \t] | Space and tab |
| [\x00-\x1F\x7F] | Control characters |
| [\x21-\x7E] | Visible characters |
| [\x20-\x7E] | Visible characters and spaces |
| [!"#$%&'()*+,-./:;<=>?@\[\]_`{|}~] | Punctuation characters |
| [ \t\r\n\v\f] | Whitespace characters |
| \w+([.-+]?\w+)*@\w+([.-]\w+)*\.\w+([.-]\w+)* | Email address |
| http(s)?://([\w-]+\.)+([\w-]+)(/[\w- ./?%&=]*)? | Internet URL |
| \(\(\d{3}\)\s?\)?\|\d{3}-\)?\d{3}-\d{3} | U.S. phone number |
| \d{3}-\d{2}-\d{4} | U.S. Social Security number |
| \d{5}(-\d{4})? | U.S. ZIP code |