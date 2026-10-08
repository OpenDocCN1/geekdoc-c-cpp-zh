Unfortunately, the code above is messy and rather special-purpose. What would we do if we had another definition of punctuation? Let's provide a more general and useful way of removing unwanted characters from an input stream. What would that be? What would we like our user code to look like? How about

```
ps.whitespace(";:,.");  // treat semicolon, colon, comma, and dot as whitespace
for (string word; ps>>word; )
    vs.push_back(word);
```

How would we define a stream that would work like ps? The basic idea is to read words from an ordinary input stream and then treat the user-specified “whitespace” characters as whitespace; that is, we do not give “whitespace” characters to the user, we just use them to separate words. For example,

as.not
should be the two words

+   as
not

We can define a class to do that for us. It must get characters from an `istream` and have a `>>` operator that works just like `istream`'s except that we can tell it which characters it should consider to be whitespace. For simplicity, we will not provide a way of treating existing whitespace characters (space, newline, etc.) as non-whitespace; we'll just allow a user to specify additional “whitespace” characters. Nor will we provide a way to completely remove the designated characters from the stream; as before, we will just turn them into whitespace. Let's call that class `Punct_stream`:

```
class Punct_stream {   // like an istream, but the user can add to
                       // the set of whitespace characters
    public:
        Punct_stream(istream& is)
            : source(is), sensitive(true) { }

        void whitespace(const string& s)     // make s the whitespace set
        { white = s; }
        void add_white(char c) { white += c; }  // add to the whitespace set
        bool is_whitespace(char c);          // is c in the whitespace set?
    };
```