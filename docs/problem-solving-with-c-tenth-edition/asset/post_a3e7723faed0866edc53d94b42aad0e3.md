
## DISPLAY 8.6 A string Object Can Behave Like an Array

```cpp
//Demonstrates using a string object as if it were an array.
#include <iostream>
#include <string>
using namespace std;
int main()
{
    string firstName, lastName;
    cout << "Enter your first and last name:\n";
    cin >> firstName >> lastName;
    cout << "Your last name is spelled:\n";
    int i;
    for (i = 0; i < lastName.length(); i++)
    {
        cout << lastName[i] << " ";
        lastName[i] = '-';
    }
    cout << endl;
    for (i = 0; i < lastName.length(); i++)
        cout << lastName[i] << " ";  //Places a "-" under each letter.
    cout << endl;
    cout << "Good day " << firstName << endl;
    return 0;
}
```

### Sample Dialogue

```text
Enter your first and last name:
John Crichton
Your last name is spelled:
C r i c h t o n
_ _ _ _ _ _ _ _
Good day John
```

a[i], you use a.at(i); and the at member function checks to see if i evaluates to an illegal index. If the value of i in a.at(i) is an illegal index, then you should get a run-time error message telling you what is wrong. In the following two example code fragments, the attempted access is out of range, yet the first of these probably will not produce an error message, although it will be accessing a nonexistent indexed variable:

```cpp
string str("Mary");
cout << str[6] << endl;
```

The second example, however, will cause the program to terminate abnormally, so you at least know that something is wrong:

```cpp
string str("Mary");
cout << str.at(6) << endl;
```

But be warned that some systems give very poor error messages when str.at(i) has an illegal index i.

You can change a single character in the string by assigning a char value to the indexed variable, such as str[i]. This may also be done with the member function at. For example, to change the third character in the string object str to 'X', you can use either of the following code fragments:

```cpp
str.at(2) = 'X';
```
or
```cpp
str[2] = 'X';
```

As in an ordinary array of characters, character positions for objects of type string are indexed starting with 0, so the third character in a string is in index position 2.

Display 8.7 gives a partial list of the member functions of the class string. In many ways, objects of the class string are better behaved than the C strings we introduced in Section 8.1. In particular, the `==` operator on objects of the string class returns a result that corresponds to our intuitive notion of strings being equal—namely, it returns true if the two strings contain the same characters in the same order, and returns false otherwise. Similarly, the comparison operators `<`, `>`, `<=`, `>=` compare string objects using lexicographic ordering. (Lexicographic ordering is alphabetic ordering using the order of symbols given in the ASCII character set in Appendix 3. If the strings consist of all letters and are both either all uppercase or all lowercase letters, then for this case lexicographic ordering is the same as everyday alphabetical ordering.)

## DISPLAY 8.7 Member Functions of the Standard Class string

| Example | Remarks |
|---|---|
| **Constructors** |  |
| string str; | Default constructor creates empty string object str. |
| string str("sample"); | Creates a string object with data "sample". |
| string str(aString); | Creates a string object str that is a copy of aString; aString is an object of the class string. |
| **Accessors** |  |
| str[i] | Returns read/write reference to character in str at index i. Does not check for illegal index. |
| str.at(i) | Returns read/write reference to character in str at index i. Same as str[i], but this version checks for illegal index. |
| str.substr(position, length) | Returns the substring of the calling object starting at position and having length characters. |
| str.length( ) | Returns the length of str. |
| **Assignment/Modifiers** |  |
| str1 = str2; | Initializes str1 to str2's data |
| str1 += str2; | Character data of str2 is concatenated to the end of str1. |
| str.empty( ) | Returns true if str is an empty string; false otherwise. |
| str1 + str2 | Returns a string that has str2's data concatenated to the end of str1's data |
| str.insert(pos, str2); | Inserts str2 into str beginning at position pos. |
| str.erase(pos, length); | Removes substring of size length, starting at position pos. |
| **Comparison** |  |
| `str1 == str2`<br>`str1 != str2` | Compare for equality or inequality; returns a Boolean value. |
| `str1 < str2`<br>`str1 > str2` | Four comparisons. All are lexicographical comparisons. |
| `str1 <= str2`<br>`str1 >= str2` |  |
| **Finds** |  |
| str.find(str1) | Returns index of the first occurrence of str1 in str. If str1 is not found, then the special value string::npos is returned. |
| str.find(str1, pos) | Returns index of the first occurrence of string str1 in str; the search starts at position pos. |
| str.find_first_of(str1, pos) | Returns the index of the first instance in str of any character in str1, starting the search at position pos. |
| str.find_first_not_of (str1, pos) | Returns the index of the first instance in str of any character not in str1, starting the search at position pos. |

## PROGRAMMING EXAMPLE: Palindrome Testing

A palindrome is a string that reads the same front to back as it does back to front. The program in Display 8.8 tests an input string to see if it is a palindrome. Our palindrome test will disregard all spaces and punctuations and will consider upper- and lowercase versions of a letter to be the same when deciding if something is a palindrome. Some palindrome examples are as follows:

- Able was I ere I saw Elba.
- I Love Me, Vol. I.
- Madam, I'm Adam.
- A man, a plan, a canal, Panama.
- Rats live on no evil star.
- radar
- deed
- mom
- racecar

The removePunct function is of interest in that it uses the string member functions substr and find. The member function substr extracts a substring of the calling object, given the position and length of the desired substring.

### DISPLAY 8.8 Palindrome Testing Program

```cpp
//Test for palindrome property.
#include <iostream>
#include <string>
#include <cctype>
using namespace std;

void swap (char& v1, char& v2);
//Interchanges the values of v1 and v2.

string reverse(const string& s);
//Returns a copy of s but with characters in reverse order.

string removePunct(const string& s, const string& punct);
//Returns a copy of s with any occurrences of characters
//in the string punct removed.

string makeLower(const string& s);
//Returns a copy of s that has all uppercase
//characters changed to lowercase, other characters unchanged.

bool isPal(const string& s);
//Returns true if s is a palindrome, false otherwise.

int  main()
{
    string str;
    cout << "Enter a candidate for palindrome test\n"
        << "followed by pressing Return.\n";
    getline(cin, str);

    if (isPal(str))
        cout << "\"" <<str + "\" is a palindrome.";
    else
        cout << "\"" <<str + "\" is not a palindrome.";
    cout << endl;

    return 0;
}

void swap(char& v1, char& v2)
{
    char temp = v1;
    v1 = v2;
    v2 = temp;
}

string reverse(const string& s)
{
    int start = 0;
    int end = s.length();
    string temp(s);

    while (start < end)
    {
        end--;
        swap(temp[start], temp[end]);
        start++;
    }

    return temp;
}

//Uses <cctype> and <string>
string makeLower(const string& s)
{
    string temp(s);
    for (int i = 0; i < s.length(); i++)
        temp[i] = tolower(s[i]);

    return temp;
}

string removePunct(const string& s, const string& punct)
{
    string noPunct; //initialized to empty string
    int sLength = s.length();
    int punctLength = punct.length();
```
