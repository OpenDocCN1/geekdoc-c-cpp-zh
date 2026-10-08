# Chapter 21

# Characters and Strings II

We've talked about how char types are actually just integer types... but it's the same for a character in single quotes.

But a string in double quotes is type const char *.

Turns out there are few more of strings and characters, and it leads down one of the most infamous rabbit holes in the language: the whole multibyte/wide/Unicode/localization thing.

We're going to peer into that rabbit hole, but not go in. ...Yet!

# 21.1 Escape Sequences

We're used to strings and characters with regular letters, punctuation, and numbers:

But if we want we some special characters in there that we can't type on the keyboard because they don't exist (e.g. "\

```
char t = '\\';
```

To do these, we use something called escape sequences. These are the backslash character (\) followed by another character. The two (or more) characters together have special meaning.

For our single quote character example, we can put an escape (that is, \) in front of the central single quote to solve it:

```
char t = '\\';
```

Now C knows that \ means just a regular character we want to print, not the end of the sequence.

You can say either "\backslash" or "escape" in this context ("escape quote") and C devs will know what you're talking. Also, "escape" in this context is different from your Esc key or the ASCII code.

# 21.1.1 Frequently-used escapes

In my humble opinion, these escape characters make up 99.2%¹ of all escapes.