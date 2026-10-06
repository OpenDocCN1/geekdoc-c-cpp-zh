The string returned by trimmed() is

```
BOB|\t|THE|\nDOG
```

When handling user input, we often also want to replace every sequence of one or more internal whitespace characters with single spaces, in addition to stripping whitespace from both ends. This is what the simplified() function does:

```
QString str = " BOB \t THE \nDOG \n"
debug() << str.simplified();
```

The string returned by simplified()

```
BOB|THE|DOG
```

A string can be split into a QStringList of substrings using QString::split():

```
QString str = "polluter pays principle"
QStringList words = str.split(" ");
```

In the preceding example, we split the string "polluter pays principle" into three substrings: "polluter", "pays", and "principle". The split() function has an optional argument that specifies whether empty substrings should be kept (the default) or discarded.

The items in a QStringList can be joined to form a single string using join(). The argument to join() is inserted between each pair of joined strings. For example, here's how to create a single string that is composed of all the strings contained in a QStringList sorted into alphabetical order and separated by newlines:

```
words.sort();
str = words.join("\n");
```

When dealing with strings, we often need to determine whether a string is empty or not. This is done by calling isEmpty() or by checking whether length() is 0.

The conversion from const char * strings to QString is automatic, in most cases,