
tokenizing an expression (§7.8.2). For example, we want `1+4*x<=y/z*5` to be separated into the eleven tokens

```cpp
1 + 4 * x <= y / z * 5
```

We could use `>>` to read the numbers, but trying to read the identifiers as strings would cause `x<=y` to be read as one string (since `<` and `=` are not whitespace characters) and `z*` to be read as one string (since `*` isn't a whitespace character either). Instead, we could write

```cpp
for (char ch; cin.get(ch); ) {
    if (isspace(ch)) {       // if ch is whitespace
        // do nothing (i.e., skip whitespace)
    }
    if (isdigit(ch)) {
        // read a number
    }
    else if (isalpha(ch)) {
        // read an identifier
    }
    else {
        // deal with operators
    }
}
```

The `istream::get()` function reads a single character into its argument. It does not skip whitespace. Like `>>`, `get()` returns a reference to its `istream` so that we can test its state.

When we read individual characters, we usually want to classify them: Is this character a digit? Is this character uppercase? And so forth. There is a set of standard library functions for that:

### Character classification

| Function | Description |
|---|---|
| `isspace(c)` | Is `c` whitespace (' ', '\t', '\n', etc.)? |
| `isalpha(c)` | Is `c` a letter ('a'...'z', 'A'...'Z') (note: not '_')? |
| `isdigit(c)` | Is `c` a decimal digit ('0'...'9')? |
| `isxdigit(c)` | Is `c` a hexadecimal digit (decimal digit or 'a'..'f' or 'A'..'F')? |
| `isupper(c)` | Is `c` an uppercase letter? |
| `islower(c)` | Is `c` a lowercase letter? |
| `isalnum(c)` | Is `c` a letter or a decimal digit? |
| `iscntrl(c)` | Is `c` a control character (ASCII 0..31 and 127)? |
| `ispunct(c)` | Is `c` not a letter, digit, whitespace, or invisible control character? |
| `isprint(c)` | Is `c` printable (ASCII `'!'... '~'`)? |
| `isgraph(c)` | Is `isalpha(c)` or `isdigit(c)` or `ispunct(c)` (note: not space)? |

Note that the classifications can be combined using the “or” operator (\|\|). For example, `isalnum(c)` means `isalpha(c)||isdigit(c)`; that is, “Is `c` either a letter or a digit?”

In addition, the standard library provides two useful functions for getting rid of case differences:

### Character case

| Function | Description |
|---|---|
| `toupper(c)` | `c` or `c`’s uppercase equivalent |
| `tolower(c)` | `c` or `c`’s lowercase equivalent |

These are useful when you want to ignore case differences. For example, in input from a user `Right`, `right`, and `rigHT` most likely mean the same thing (`rigHT` most likely being the result of an unfortunate hit on the Caps Lock key). After applying `tolower()` to each character in each of those strings, we get `right` for each. We can do that for an arbitrary `string`:

```cpp
void tolower(string& s)        // put s into lower case
{
    for (char& x : s) x = tolower(x);
}
```

We use pass-by-reference (§8.5.5) to actually change the `string`. Had we wanted to keep the old string we could have written a function to make a lowercase copy. Prefer `tolower()` to `toupper()` because that works better for text in some natural languages, such as German, where not every lowercase character has an uppercase equivalent.

## 11.7 Using nonstandard separators

This section provides a semi-realistic example of the use of `iostreams` to solve a real problem. When we read strings, words are by default separated by whitespace. Unfortunately, `istream` doesn’t offer a facility for us to define what characters make up whitespace or in some other way directly change how `>>` reads a string. So, what do we do if we need another definition of whitespace? Consider the

example from §4.6.3 where we read in “words” and compared them. Those words were whitespace-separated, so if we read

> *As planned, the guests arrived; then,*

We would get the “words”

- * As
- planned,
- the
- guests
- arrived;
- then,

This is not what we’d find in a dictionary: `planned,` and `arrived;` are not words. They are words plus distracting and irrelevant punctuation characters. For most purposes we must treat punctuation just like whitespace. How might we get rid of such punctuation? We could read characters, remove the punctuation characters — or turn them into whitespace — and then read the “cleaned-up” input again:

```cpp
string line;
getline(cin, line);        // read into line
for (char& ch : line)      // replace each punctuation character by a space
    switch(ch) {
        case ';': case '.': case ',': case '?': case '!':
            ch = ' ';
    }

stringstream ss(line);   // make an istream ss reading from line
vector<string> vs;
for (string word; ss >> word; ) // read words without punctuation characters
    vs.push_back(word);
```

Using that to read the line, we get the desired

- * As
- planned
- the
- guests
- arrived
- then

Unfortunately, the code above is messy and rather special-purpose. What would we do if we had another definition of punctuation? Let's provide a more general and useful way of removing unwanted characters from an input stream. What would that be? What would we like our user code to look like? How about

```cpp
ps.whitespace(";:,.");  // treat semicolon, colon, comma, and dot as whitespace
for (string word; ps >> word; )
    vs.push_back(word);
```

How would we define a stream that would work like `ps`? The basic idea is to read words from an ordinary input stream and then treat the user-specified “whitespace” characters as whitespace; that is, we do not give “whitespace” characters to the user, we just use them to separate words. For example,

as.not

should be the two words

- as
- not

We can define a class to do that for us. It must get characters from an `istream` and have a `>>` operator that works just like `istream`'s except that we can tell it which characters it should consider to be whitespace. For simplicity, we will not provide a way of treating existing whitespace characters (space, newline, etc.) as non-whitespace; we'll just allow a user to specify additional “whitespace” characters. Nor will we provide a way to completely remove the designated characters from the stream; as before, we will just turn them into whitespace. Let's call that class `Punct_stream`:

```cpp
class Punct_stream {   // like an istream, but the user can add to
                       // the set of whitespace characters
    public:
        Punct_stream(istream& is)
            : source(is), sensitive(true) { }

        void whitespace(const string& s)     // make s the whitespace set
        { white = s; }
        void add_white(char c) { white += c; }  // add to the whitespace set
        bool is_whitespace(char c);          // is c in the whitespace set?

        void case_sensitive(bool b) { sensitive = b; }
        bool is_case_sensitive() { return sensitive; }

        Punct_stream& operator>>(string& s);
        operator bool();

    private:
        istream& source;           // character source
        istringstream buffer;     // we let buffer do our formatting
        string white;             // characters considered "whitespace"
        bool sensitive;          // is the stream case-sensitive?
};
```

The basic idea is — just as in the example above — to read a line at a time from the `istream`, convert “whitespace” characters into spaces, and then use the `istringstream` to do formatting. In addition to dealing with user-defined whitespace, we have given `Punct_stream` a related facility: if we ask it to, using `case_sensitive()`, it can convert case-sensitive input into non-case-sensitive input. For example, if we ask, we can get a `Punct_stream` to read

**Man bites dog!**

as

- man
- bites
- dog

`Punct_stream`’s constructor takes the `istream` to be used as a character source and gives it the local name `source`. The constructor also defaults the stream to the usual case-sensitive behavior. We can make a `Punct_stream` that reads from `cin` regarding semicolon, colon, and dot as whitespace, and that turns all characters into lower case:

```cpp
Punct_stream ps(cin);          // ps reads from cin
ps.whitespace(";:.");        // semicolon, colon, and dot are also whitespace
ps.case_sensitive(false);     // not case-sensitive
```

Obviously, the most interesting operation is the input operator `>>`. It is also by far the most difficult to define. Our general strategy is to read a whole line from the `istream` into a string (called `line`). We then convert all of “our” whitespace characters to the space character (' '). That done, we put the line into the `istringstream`
