C-style strings will say that phrase has a length of 12, which makes sense and is in line with how string objects work.)

As with any other type of array, you can specify the array size when you define it. So another way to declare and initialize a C-style string is

```
char phrase[81] = "Game Over!!!";
```

The previous code creates a C-style string that can hold 80 printable characters (plus its terminating null character).

C-style strings don't have member functions. But the cstring file, which is part of the standard library, contains a variety of functions for working with C-style strings.

A nice thing about string objects is that they're designed to work seamlessly with C-style strings. For example, all of the following are completely valid uses of C-style strings with string objects:

```
string word1 = "Game";
char word2[] = " Over";

string phrase = word1 + word2;

if (word1 != word2)
{
    cout << "word1 and word2 are not equal.\n";
}

if (phrase.find(word2) != string::npos)
{
    cout << "word2 is contained in phrase.\n";
}
```

You can concatenate string objects and C-style strings, but the result is always a string objet (so the code char phrase2[] = word1 + word2; would produce an error). You can compare string objects and C-style strings using the relational operators. And you can even use C-style strings as arguments in string object member functions.

C-style strings have the same shortcomings as arrays. One of the biggest is that their lengths are fixed. So the moral is: Use string objects whenever possible, but be prepared to work with C-style strings if necessary.