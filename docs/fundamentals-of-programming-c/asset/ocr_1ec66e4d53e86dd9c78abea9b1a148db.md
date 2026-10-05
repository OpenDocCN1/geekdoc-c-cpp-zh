# 13.1. STRING OBJECTS

```
cout << "not equal" << endl;
cout << "Compare " << first << " and XYZ":
if (first == "XYZ")
    cout << "equal" << endl;
else
    cout << "not equal" << endl;
```

The statement

```
word = "good";
```

is equivalent to

```
word.operator=("good");
```

Here we see the explicit use of the dot (,) operator to invoke the method. Similarly,

```
word += "-bye";
```

is the syntactically sweetened way to write

```
word.operator+=("-bye");
```

The + operator performs string concatenation, making a new string by appending one to the back of another.

With the substr we can extract a new string from another, as shown in Figure 13.1.

```
string word = "Good-bye";
string other = word.substr(2, 5);
word
```

![](bbox=[0.31342000000000003, 0.6035499999999999, 0.61642, 0.76355])

In addition to string methods, the standard string library provides a number of global functions that process strings. These functions use operator syntax and allow us to compare strings using <, ==, >=, etc. A more complete list of string methods and functions can be found at http://www.cplusplus.com/reference/string/