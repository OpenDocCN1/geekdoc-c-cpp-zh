# Note

Older versions of get(char *, int) don’t evaluate to false upon reading an empty line. For those versions, however, the first character in the string is a null character if an empty line is entered. This example uses the following code:

```
if (!cin || temp[0] == '\0')    // empty line?
    break;                       // i not incremented
```

If the implementation follows the current C++ Standard, the first test in the if statement detects an empty line, whereas the second test detects the empty line for older implementations.

The program in Listing 12.6 asks the user to enter up to 10 sayings. Each saying is read into a temporary character array and then copied to a String object. If the user enters a blank line, a break statement terminates the input loop. After echoing the input, the program uses the length() and operator<() member functions to locate the shortest string and the alphabetically earliest string. The program also uses the subscript operator ([]) to preface each saying with its initial character. Here’s a sample run:

```
Hi, what's your name?
>> Misty Gutz
Misty Gutz, please enter up to 10 short sayings <empty line to quit>:
1: a fool and his money are soon parted
2: penny wise, pound foolish
3: the love of money is the root of much evil
4: out of sight, out of mind
5: absence makes the heart grow fonder
6: absinthe makes the hart grow fonder
7:
Here are your sayings:
a: a fool and his money are soon parted
p: penny wise, pound foolish
t: the love of money is the root of much evil
o: out of sight, out of mind
a: absence makes the heart grow fonder
a: absinthe makes the hart grow fonder
Shortest saying:
penny wise, pound foolish
First alphabetically:
a fool and his money are soon parted
This program used 11 String objects. Bye.
```