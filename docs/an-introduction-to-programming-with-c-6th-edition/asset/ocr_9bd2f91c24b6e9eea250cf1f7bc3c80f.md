# CHAPTER 13 Strings

# HOW TO Use the replace Function

Syntax
string.replace(substring, count, replacementString);

Example 1
string phone = "1-800-111-0000";
phone.replace(2, 3, "877");
replaces three characters in the phone variable, beginning with the
character whose subscript is 2, with "877"; changes the contents of the
phone variable to "1-877-111-0000"

Example 2
string item = "ABC34";
item.replace(3, 1, "D");
replaces one character in the item variable, beginning with the character
whose subscript is 3, with "D", changes the contents of the item variable to
"ABCD34"

Example 3
string name = "Karen Wilson";
name.replace(7, 6, "Farley");
replaces six characters in the name variable, beginning with the character
whose subscript is 7, with "Farley", changes the contents of the
variable to "Karen Farley"

```
Example 4
int subscript = 0;
string salary = "";
cout << "Salary:";
geteline(cin, salary);
while (subscript < salary.length()) == ""
    if (salary.substr(subscript, 1) == " \)
        salary.replace(subscript, 1, "");
    else
        subscript += 1;
    //end if
// while
```

replaces the empty string with any commas and spaces for the
variable

Figure 13-28 How to use the replace function

Figure 13-29 shows how you can use the replace function, instead of the
erase function, in the annual income program. The modification made to
t original code (shown earlier in Figure 13-26) is shaded in Figure 13-29.

552