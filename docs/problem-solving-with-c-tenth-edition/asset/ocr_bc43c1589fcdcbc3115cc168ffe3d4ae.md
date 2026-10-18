# PROGRAMMING EXAMPLE
Palindrome Testing

A palindrome is a string that reads the same front to back as it does back to front. The program in Display 8.8 tests an input string to see if it is a palindrome. Our palindrome test will disregard all spaces and punctuations and will consider upper- and lowercase versions of a letter to be the same when deciding if something is a palindrome. Some palindrome examples are as follows:

+   - Able was I ere I saw Elba.
+   - I Love Me, Vol. I.
+   - Madam, I'm Adam.
+   - A man, a plan, a canal, Panama.
+   - Rats live on no evil star.
+   - radar
+   - deed
+   - mom
+   - racecar

The removePunct function is of interest in that it uses the string member functions substr and find. The member function substr extracts a substring of the calling object, given the position and length of the desired substring.

# DISPLAY 8.8 Palindrome Testing Program (part 1 of 3)

```
1  //Test for palindrome property.
2  #include <iostream>
3  #include <string>
4  #include <cctype>
5  using namespace std;
6  
7  void swap (char& v1, char& v2);
8  //Interchanges the values of v1 and v2.
9  
10 string reverse(const string& s);
11 //Returns a copy of s but with characters in reverse order.
12 
13 string removePunct(const string& s, const string& punct);
14 //Returns a copy of s with any occurrences of characters
15 //in the string punct removed.
16 
17 string makeLower(const string& s);
18 //Returns a copy of s that has all uppercase
19 //characters changed to lowercase, other characters unchanged.
20 
21 bool isPal(const string& s);
22 //Returns true if s is a palindrome, false otherwise.
23 
24 int  main()
25 {
26     string str;
(continued)
```