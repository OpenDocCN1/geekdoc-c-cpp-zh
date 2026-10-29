# 25. What is the output produced by the following code?

```
string s1, s2("Hello");
s1 = s2;
s2[0] = 'j';
cout << s1 << " " << s2;
```

# CONVERTING BETWEEN string OBJECTS AND C-STRINGS

You have already seen that C++ will perform an automatic type conversion to allow you to store a C-string in a variable of type string. For example, the following will work fine:

```
char aCString[] = "This is my C-string.";
string stringVariable;
stringVariable = aCString;
```

However, the following will produce a compiler error message:

```
aCString = stringVariable; //ILLEGAL
```

The following is also illegal:

```
strcpy(aCString, stringVariable); //ILLEGAL
```

strcpy cannot take a string object as its second argument and there is no automatic conversion of string objects to C-strings, which is the problem we cannot seem to get away from.

To obtain the C-string corresponding to a string object you must perform an explicit conversion. This can be done with the string member function c_str(). The correct version of the copying we have been trying to do is the following:

```
strcpy(aCString, stringVariable.c_str()); //Legal;
```

Note that you need to use the strcpy function to do the copying. The member function c_str() returns the C-string corresponding to the string calling object. As we noted earlier in this chapter, the assignment operator does not work with C-strings. So, just in case you thought the following might work, we should point out that it too is illegal.

```
aCString = stringVariable.c_str(); //ILLEGAL
```