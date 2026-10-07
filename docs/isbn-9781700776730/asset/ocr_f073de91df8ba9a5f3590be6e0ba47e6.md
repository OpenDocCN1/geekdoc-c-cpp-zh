# Overloading Operator []

As you know, in C the operator [] is typically used to represent indexing. That is, the value between the square brackets specifies which element of the designated array is referenced. Of course, if you were to attempt to apply the bracket operator to an some user-defined class, the compiler would complain because it has no idea what you are trying to do. However, you may give it meaning for your class by overloading it. Typically this would be done for a class that contains an array or a pointer as a data member. The big advantage here is that having your own function allows you to do a validity check on the index value. Recall that operator[] must be a binary member (not friend) function of the class. In other words, there must be one explicit argument which is the index value itself. In the case of the String class, the [] operator function will be used to fetch a particular character from the array of characters.

```
char& operator[](int index);
```

Note that the character is being returned by reference. The validity of the index value should be checked. If it turns out to be invalid, the function should output an error message and return `NULL` value.

# Bracket vs. Pointer Notation

The use of brackets in C is just a convenience for you that avoids your having to use pointer dereferencing when accessing an array element. In other words, for some array s, the three constructs should all yield the same result since they are equivalent:

| s[i] | *(s + i) |

Thus, it is incumbent upon you to allow the user of the String class to be able to write code using the latter two notations. As thing stand now, the compiler would complain because it has no idea how to add a String object and an int. Therefore, the + operator must be overloaded again to accommodate both syntax forms.

```
friend char* operator+(const String&, int);
friend char* operator+(int, const String&);
```