# Program 12: Using the SUBSTR Function to Extract Substrings

```
data Extract;
input ID : $10. @@;
length State $ 2 Gender $ 1 Last $ 5;
State = ID;
Number = input(substr(ID,3,2),);
gender = substr(ID,5,1);
Last = substr(ID,6);
datalines;
NJ12M99 NY76F4512 TX91M5
```

The first argument to this function is the string you are searching. The second and third arguments of the SUBSTR function specify the starting position and the length of the substring. For example, the variable Gender is extracted from ID, starting in the fifth position for a length of 1. The variable Name is bit more complicated. The SUBSTR function extracts two digits, starting at Position 3, and then uses the INPUT function to perform a character-to-numeric conversion. Notice that the SUBSTR function used to create the variable Last does not use a argument; missing the SUBSTR function extracts characters until the last non-blank character in the string.

Wait! What about State? Why wasn't the SUBSTR function used in assignment statement? Notice that the variable State is declared as a character with a length of 2 in the LENGTH statement. When you set State to ID, because the storage length of State is 2, it contains the first two characters of the variable ID. This is a nice "trick" used by many SAS programmers. The reason it is preferred to using the SUBSTR function is that functions use computer resources (CPU time) and this trick avoids using functions. (Once again, the author's compulsive programming personality shows through.)

Here is a list of the resulting data set:

# Figure 12.14: Listing of Data Set Extract

| ID | State | Gender | Last | Number |
|---|---|---|---|---|
| NJ12M99 | NJ | M | 99 | 12 |
| NJ76F4512 | NY | F | 4512 | 76 |
| TX91M5 | TX | M | 5 | 91 |

In this program, a LENGTH statement is used to define the lengths of State, Gender, and Last. Without this statement, the lengths of these three character variables would be equal to 10, that is the length of ID. Understanding why is very important.

SAS assigns a length to all character variables in the compile stage before any data values are read. In general, the starting position and the length of a substring could be read from data or computed in the DATA step. So, without a LENGTH statement, what length should SAS assign to the variables State, Gender, and Last? The longest substring you can extract from a string of length n is a string of length n, so if you don't define a length, that's exactly SAS does.