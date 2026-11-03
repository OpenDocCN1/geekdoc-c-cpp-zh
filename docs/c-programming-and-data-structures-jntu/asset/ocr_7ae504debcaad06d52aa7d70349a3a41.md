while the statement

```
strcat(part1, part3);
```

will result in:

![](bbox=[0.2, 0.3, 0.92, 0.38])

![](bbox=[0.25, 0.41, 0.65, 0.48])

We must make sure that the size of string1 (to which string2 is appended) is large enough to accommodate the final string.

strcat function may also append a string constant to a string variable. The following is valid.

```
strcat(part1, "GOOD");
```

C permits nesting of strcat functions. For example, the statement

```
strcat(strcat(string1,string2), string3);
```

is allowed and concatenates all the three strings together. The resultant string is stored in string1.

# strcmp( ) Function

The strcmp function compares two strings identified by the arguments and has a value 0 if they are equal. If they are not, it has the numeric difference between the first nonmatching characters in the strings. It takes the form:

```
strcmp(string1, string2);
```

string1 and string2 may be string variables or string constants. Examples are:

```
strcmp(name1, name2);
strcmp(name1, "John");
strcmp("Rom", "Ram");
```

Our major concern is to determine whether the strings are equal; if not, which is alphabetically above. The value of the mismatch is rarely important. For example, the statement

```
strcmp("their", "there");
```

will return a value of -9 which is the numeric difference between ASCII "i" and ASCII "r". That is, "i" minus "r" in ASCII code is -9. If the value is negative, string1 is alphabetically above string2.

# strcpy( ) Function

The strcpy function works almost like a string-assignment operator. It takes the form

```
strcpy(string1, string2);
```