```
cin.clear(); // reset stream state
while (!isspace(cin.get()))
    continue; // get rid of bad input
}
else // bail out
{
    cout << "I cannot go on!\n";
    exit(1);
}
cout << "Now enter a new number: ";
cin >> input; // will work now
```

# Other istream Class Methods

Chapters 3 to 5 discuss the get () and getline () methods. As you may recall, they provide the following additional input capabilities:

+   - The get (char \) and get (void) methods provide single-character input that doesn't skip over white space.
- The get (char *, int, char) and getline(char *, int, char) functions by default read entire lines rather than single words.

These are unformatted input functions because they simply read character as is, without skipping over white space and without performing data conversions.
Let's look at these two groups of istream class member functions.

# Single-Character Input

When used with a char argument or no argument at all, the get () methods fetch the next input character, even if it is a space, tab, or newline character. The get (char & ch) version assigns its input character to its argument, and the get (void) version uses the input character, converted to an integer (typically int), as its return value.

# The get (char &) Member Function

Let's try get (char &) first. Suppose you have the following loop in program:

```
int ct = 0;
char ch;
cin.get(ch);
while (ch != '\\n')
{
    cout << ch;
    ct++;
    cin.get(ch);
}
```

cout << ct << endl;