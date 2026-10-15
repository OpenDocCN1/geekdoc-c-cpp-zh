Because a string is an array of characters, we can access individual characters in a string directly with array subscript notation. For example, string1[ 0 ] is the character 'f', string1[ 3 ] is the character 's' and string1[ 5 ] is the null character.
We can input a string directly into a character array from the keyboard using cin and >>. For example, the declaration

```
char string2[ 20 ];
```

creates a character array capable of storing a string of up to 19 characters and a terminating null character. The statement

```
cin >> string2;
```

reads a string from the keyboard into string2 and appends the null character to the end of the string input by the user. Note that the preceding statement provides only the name of the array and no information about the size of the array. It is your responsibility to ensure that the array into which the string is read is capable of holding any string the user types at the keyboard. By default, cin reads characters from the keyboard until the first white-space character is encountered—regardless of the array size. Thus, inputting data with cin and >> can insert data beyond the end of the array (see Section 8.13 for information on preventing insertion beyond the end of a char array).

# Common Programming Error 7.9

> Not providing cin >> with a character array large enough to store a string typed at the keyboard can result in loss of data in a program and other serious runtime errors.

A character array representing a null-terminated string can be output with cout and <<. The statement

```
cout << string2;
```

prints the array string2. Note that cout <<, like cin >>, does not care how large the character array is. The characters of the string are output until a terminating null character is encountered; the null character is not printed. [Note: cin and cout assume that character arrays should be processed as strings terminated by null characters; cin and cout do not provide similar input and output processing capabilities for other array types.]

Figure 7.12 demonstrates initializing a character array with a string literal, reading a string into a character array, printing a character array as a string and accessing individual characters of a string.

Lines 23–24 of Fig. 7.12 use a for statement to loop through the string1 array and print its characters separated by spaces. The condition in the for statement, string1[ i ] != '\0', is true until the loop encounters the terminating null character of the string.

```
1  // Fig. 7.12: fig07_12.cpp
2  // Treating character arrays as strings.
3  #include <iostream>
4  using std::cout;
5  using std::cin;
6  using std::endl;
```

Fig. 7.12 | Character arrays processed as strings. (Part 1 of 2.)