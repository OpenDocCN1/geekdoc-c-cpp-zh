As a further example, let’s see how we can combine regular expressions to match phone numbers in one of these formats:

+   - (999) 999-9999
+   - 999-999-9999
+   - 999 999 9999

We need to match the first group of three digits. To match exactly three digits we can use \d for a digit and {3} for exactly three digits:

```
\d{3}
```

To account for the parentheses we can allow an optional left and right parenthesis. We have to use the escape character in front of the parenthesis; otherwise, the parenthesis will be interpreted as grouping for precedence. The ? after the \ matches zero or one left parenthesis and the ? after the \ ) matches zero or one right parenthesis. The regular expression so far for the first three digits with or without parentheses is

```
(\?\d{3}\)\?)
```

A dash or whitespace separates the first group of digits from the next group of three digits. We can match the dash or whitespace with the regular expression (-|\s), which becomes the following when added to the end of our regular expression:

```
(\?\d{3}\)\?)(- |\s)
```

Next we repeat a group of exactly three digits:

```
\(\?\d{3}\)\?(-|\s)\d{3}
```

Finally we have a dash or whitespace and exactly four digits:

```
\(\?\d{3}\)\?(-|\s)\d{3}(-|\s)\d{4}
```

The following lines of code output "Phone number found" because regex_search returns true if it finds a match to the regular expression anywhere in the target string:

```
string text = "Call me at (907) 867-5309";
string pattern = R"(\(\?\d{3}\)\?(-|\s)\d{3}(-|\s)\d{4})";
regex reg(pattern);

if (regex_search(text, reg))
    cout << "Phone number found" << endl;
```

Finally, if you wish to find all occurrences that match a regular expression, then you can use a regular expression iterator. The class sregex_iterator is used to iterate though all matches of the regular expression within a target string. The class regex_iterator is used for a C-style string. An example is shown below in which all phone numbers within the string are displayed. The constructor for the iterator takes the regular expression and references to the beginning and