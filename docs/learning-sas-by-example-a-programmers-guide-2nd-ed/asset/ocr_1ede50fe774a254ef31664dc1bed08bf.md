# 192 Learning SAS by Example: A Programmermer's Guide, Second Edition

As an example, suppose you want to look for the name Roger in a list of character values (ignoring case). Here is the program:

# Program 12.9: Demonstrating the FINDW Function

```
data Look_for_Roger;
input String $40;
if findw(String,'Roger,','i') then Match = 'Yes'
elelse Match = 'No';
datalines;
Will Rogers
Roger Cody
Was Roger here?
Was Roger here?;
```

Here is a listing:

# Figure 12.10: Listing of Data Set Look_for_Roger

| String | Match |
| Will Rogers | No |
| Roger Cody | Yes |
| Was Roger here? | Yes |
| Was Roger here? | Yes |

This program shows why the FINDW function is useful when you are looking for words that may be part of a longer string.

# 12.11 Searching for Character Classes

A group of functions that some call the ANY functions (ANYNUMAL, ANYPHA, ANYDIGIT, ANYPUNCT, and ANYSPACE) allow you to search for alphanumeric values (upper- and lowercase letters and digits), alphas (all letters), digits, punctuation characters, and space characters (blank, tab, line feeds), respectively.

As an example, suppose you have some ID values, some contain digits and some do not. You want to search each ID and create a list of all the IDs that contain one or more digits. The IDs are stored in a text file called ID.txt.

A listing of the ID.txt file is as follows:

```
abcABC
NJ1234
987654
123XYZ
TX78010
```