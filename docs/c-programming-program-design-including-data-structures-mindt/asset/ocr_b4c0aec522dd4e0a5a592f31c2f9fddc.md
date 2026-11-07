When `\n` is encountered in the string, the insertion point is positioned at the beginning of the next line. Note also that `\n` may appear anywhere in the string. For example, the output of the statement:

```
cout << "Hello \\nthere. \\nMy name is James.";
```

is:

```
Hello
there.
My name is James.
```

Also, note that the output of the statement:

```
cout << '\\n';
```

is the same as the output of the statement:

```
cout << "\\n";
```

which is the same as the output of the statement:

```
cout << endl;
```

Thus, the output of the sequence of statements:

```
cout << "Hello there.\\n";
cout << "My name is James.";
```

is the same as the output of the sequence of statements:

```
cout << "Hello there." << endl;
cout << "My name is James.";
```

# EXAMPLE 2-23

Consider the following C++ statements:

```
cout << "Hello there.\\nMy name is James.";
```

or:

```
cout << "Hello there.";
cout << "\\nMy name is James.";
```

or:

```
cout << "Hello there.";
cout << endl << "My name is James.";
```

In each case, the output of the statements is:

```
Hello there.
My name is James.
```