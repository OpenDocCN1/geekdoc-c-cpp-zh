+   - long
+   - unsigned long
+   - long long (C++11)
+   - unsigned long long (C++11)
+   - float
+   - double
+   - long double

The ostream class provides a definition for the operator<<() function for each of these data types. (Functions that have operator in their names are used to overload operators, as discussed in Chapter 11, “Working with Classes.”) Thus, if you use a statement of the following form, and if value is one of the preceding types, a C++ program can match it to an operator function with the corresponding signature:

```
```
cout << value;
```
```

For example, the expression cout << 88 matches the following method prototype:

```
```
ostream & operator<<(int);
```
```

Recall that this prototype indicates that the operator<<() function takes one type int argument. That’s the part that matches the 88 in the previous statement. The prototype also indicates that the function returns a reference to an ostream object. That property makes it possible to concatenate output, as in the following old rock hit:

```
```
cout << "*I'm feeling sedimentary over *" << boundary << "\n";
```
```

If you’re a C programmer who has suffered through C’s multitudinous type specifiers and the problems that arise when you mismatch a specifier type to a value, using cout is almost sinfully easy. (And C++ input, of course, is sinfully easy.)

# **Output and Pointers**

The ostream class defines insertion operator functions for the following pointer types:

+   - const signed char *
+   - const unsigned char *
+   - const char *
+   - void *

C++ represents a string, don’t forget, by using a pointer to the location of the string. The pointer can take the form of the name of an array of char or of an explicit pointer-to-char or of a quoted string. Thus, all the following cout statements display strings:

```
```
char name[20] = "Dudly Diddlemore";
char * pn = "Violet D'Amour";
cout << "Hello!";
```
```