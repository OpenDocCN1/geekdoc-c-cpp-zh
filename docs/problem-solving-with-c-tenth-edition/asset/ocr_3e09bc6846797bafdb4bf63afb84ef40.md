```
char aCString[] = "This is my C string.";
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

strcpy cannot take a string object as its second argument, and there is no automatic conversion of string objects to C strings, which is the problem we cannot seem to get away from.

To obtain the C string corresponding to a string object, you must perform an explicit conversion. This can be done with the string member function c_str( ). The correct version of the copying we have been trying to do is the following:

```
strcpy(aCString, stringVariable.c_str( ));  //Legal;
```

Note that you need to use the strcpy function to do the copying. The member function c_str( ) returns the C string corresponding to the string calling object. As we noted earlier in this chapter, the assignment operator does not work with C strings. So, just in case you thought the following might work, we should point out that it too is illegal.

```
aCString = stringVariable.c_str( );  //ILLEGAL
```

# Converting Between Strings and Numbers

Prior to C++11 it was a bit complicated to convert between strings and numbers, but in C++11 it is simply a matter of calling a function. Use stof, stod, stoi, or stol to convert a string to a float, double, int, or long, respectively. Use to_string to convert a numeric type to a string. These functions are illustrated in the following example:

```
int i;
double d;
string s;
i = stoi("35"); // Converts the string "35" to an integer 35
d = stod("2.5"); // Converts the string "2.5" to the double 2.5
s = to_string(d*2); // Converts the double 5.0 to a string "5.0000"
cout << i << " " << d << " " << s << endl;
```

The output is 35 2.5 5.0000