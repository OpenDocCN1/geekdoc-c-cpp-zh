```
```cpp
cin.get(ch);                         //Read the newline character; //Line 26
cout << endl;                                         //Line 27

cout << "Line 28: The string you entered = "
     << str1 << endl;                                 //Line 28

cout << "Line 29: Enter a sentence: ";              //Line 29
getline(cin, str2);                                   //Line 30
cout << endl;                                         //Line 31

cout << "Line 32: The sentence is: " << str2
     << endl;                                         //Line 32

}

return 0;
```
```

**Sample Run:** In the following sample run, the user input is shaded.

```
Line 3: Name = William Jacob
Line 5: str1 = Hello There
Line 7: str2 = Hello There
Line 10: str2 = Sunny Day
Line 14: str3 = Hello There
Line 16: str3 = Hello There
Line 18: str1 = Hello Mickey
Line 20: str1[6] = t
Line 22: str1 = Hello There
Line 23: Enter a string with no blanks: Programming

Line 28: The string you entered = Programming
Line 29: Enter a sentence: Testing string operations

Line 32: The sentence is: Testing string operations
```

The preceding output is self-explanatory, and its unraveling is left as an exercise for you.

# Additional string Operations

The data type `string` has a data type, `string::size_type`, and a named constant, `string::npos`, defined as follows:

|  |  |
|---|---|
| `string::size_type` | An unsigned integer (data) type |
| `string::npos` | The maximum value of the (data type) `string::size_type`, a number such as `4294967295` on many machines |

The data type `string` contains several other functions for string manipulation. The following table describes some these functions. In this table, we assume that `strVar` is a string variable and `str` is a string variable, a string constant, or a character array. (Arrays are discussed in Chapter 9.)