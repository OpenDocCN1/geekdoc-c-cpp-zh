This kind of use of getline seems to have been designed for use in a C++ quiz show rather than to meet any actual programming need, but it can come in handy sometimes.

# PITFALL Mixing cin >> variable; and getline

Take care in mixing input using cin >> variable; with input using getline. For example, consider the following code:

```
int n;
string line;
cin >> n;
getline(cin, line);
```

# getline for Objects of the Class string

The getline function for string objects has two versions:

```
istream& getline(istream& ins, string& strVar, char delimiter);
```

and

```
istream& getline(istream& ins, string& strVar);
```

The first version of this function reads characters from the istream object given as the first argument (always cin in this chapter), inserting the characters into the string variable strVar until an instance of the delimiter character is encountered. The delimiter character is removed from the input and discarded. The second version uses '\n' for the default value of delimiter; otherwise, it works the same.

These getline functions return their first argument (always cin in this chapter), but they are usually used as if they were void functions.

When this code reads the following input, you might expect the value of n to be set to 42 and the value of line to be set to a string value representing "Hello hitchhiker.":

```
42
Hello hitchhiker.
```

However, while n is indeed set to the value of 42, line is set equal to the empty string. What happened?

Using cin >> n skips leading whitespace on the input, but leaves the rest of the line, in this case just '\n', for the next input. A statement like

```
cin >> n;
```