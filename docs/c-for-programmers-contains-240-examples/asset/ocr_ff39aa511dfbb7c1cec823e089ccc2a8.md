less than string2. Because a string starting with 'T' is considered lexicographically greater than a string starting with 'H', result is assigned a value greater than 0, as confirmed by the output. A lexicon is a dictionary. When we say that a string is lexicographically less than another, we mean that the compare method uses the numerical values of the characters (see Appendix B, ASCII Character Set) in each string to determine that the first string is less than the second.

Line 45 uses an overloaded version of member function compare to compare portions of string1 and string3. The first two arguments (2 and 5) specify the starting subscript and length of the portion of string1 ("string") to compare with string3. The third argument is the comparison string. The last two arguments (0 and 5) are the starting subscript and length of the portion of the comparison string being compared (also "string"). The value assigned to result is 0 for equality, a positive number if string1 is lexicographically greater than string3 or a negative number if string1 is lexicographically less than string3. Because the two pieces of strings being compared here are identical, result is assigned 0.

Line 58 uses another overloaded version of function compare to compare string4 and string2. The first two arguments are the same—the starting subscript and length. The last argument is the comparison string. The value returned is also the same—0 for equality, a positive number if string4 is lexicographically greater than string2 or a negative number if string4 is lexicographically less than string2. Because the two pieces of strings being compared here are identical, result is assigned 0.

Line 74 calls member function compare to compare the first 3 characters in string2 to string4. Because "Hel" is less than "Hello", a value less than zero is returned.

# 18.4 Substrings

Class string provides member function substr for retrieving a substring from a string. The result is a new string object that is copied from the source string. Figure 18.3 demonstrates substr.

```
1  // Fig. 18.3: Fig18_03.cpp
2  // Demonstrating string member function substr.
3  #include <iostream>
4  using std::cout;
5  using std::endl;
6
7  #include <string>
8  using std::string;
9
10 int main()
11 {
12     string string1( "The airplane landed on time." );
13
14     // retrieve substring "plane" which
15     // begins at subscript 7 and consists of 5 characters
16     cout << string1.substr( 7, 5 ) << endl;
17     return 0;
18 } // end main
```

Fig. 18.3 | Demonstrating string member function substr. (Part 1 of 2.)