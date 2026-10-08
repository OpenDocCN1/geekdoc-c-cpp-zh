
# The ZIP Code Program

(continued)

2. repeat while (the ZIP code is not "-1")

```cpp
while (zipCode != "-1")
{
    if (zipCode.length() == 5)
    {
        cout << VALID_MSG << endl;
        int sub = 0;
        while (sub < zipCode.length() && foundNonNumber != 'N')
        {
            if (zipCode.substr(sub, 1) < "0" || zipCode.substr(sub, 1) > "9")
            {
                foundNonNumber = 'N';
            }
            else
            {
                sub += 1;
            }
        }
        //end while
        if (foundNonNumber == 'N')
        {
            cout << ALL_NUMBERS << endl;
        }
        else
        {
            cout << NOT_NUMBERS << endl;
        }
        //end if
    }
    else
    {
        cout << INVALID_MSG << endl;
        //end if
        cout << "Five-character ZIP code (-1 to end): ";
        cin >> zipCode;
    }
}
//end while
```

if (the ZIP code contains
exactly 5 characters)
display "Valid length" message

assign 0 to character subscript

repeat while (the character subscript
is less than the number of characters
in the ZIP code, and the variable
keeps track of whether a
non-numeric character appears
in the ZIP code contains 'N')

if (the current character
in the ZIP code is less than
"0" or greater than "9")

assign 'Y' to the variable
keeps track of whether
a non-numeric character
appears in the ZIP code

add 1 to the character
subscript

end if
repeat while

if (the variable that keeps track of
whether a non-numeric character
appears in the ZIP code contains 'N')
display the "All numbers"
message

display the "Not all
numbers" message

end if
else

display the "Invalid length"
message

end if
enter the ZIP code

Figure 13-17 Modified problem specification, IPO chart information, and C++ instructions for the ZIP code problem

The modified ZIP code program is shown in Figure 13-18, with the modification made to the original program (earlier in Figure 13-14) shaded. Figure 13-19 shows a sample run of the modified program.

![](img/d64a28a68f49d61137bf2f3170ac40ad_561_0.png)

# CHAPTER 13 Strings

```cpp
1 // Modified ZIP Code.cpp
2 //Displays a message indicating whether a ZIP
3 //code's length is valid or invalid. Also displays
4 //message indicating whether each character
5 //in the ZIP code is a number
6 //Created/by your <name> on current date>
7
8 #include <iostream>
9 #include <string>
10 using namespace std;
11
12 int main() {
13
14 const string VALID_MSG = "Valid length";
15 const string INVALID_MSG = "Invalid length";
16 const string ALL_NUMBERS = "All numbers";
17 const string NOT_ALL_NUMBERS = "Not all numbers";
18 string zipCode;
19 char foundNumber
20 = "N";
21
22 cout << "Five-character ZIP code (-1 to end): ";
23 cin >> zipCode;
24
25
26 while (zipCode != "-1") {
27
28 if (zipCode.length() == 5) {
29 cout << VALID_MSG << endl;
30 //determine msg whether each character
31 //is a number
32 int sub = 0;
33 while (sub < zipCode.length()
34 && foundNumber == 'N') {
35 if (zipCode.substr(sub, 1) >= "0" &&
36 //zipCode.substr(sub, 1) <= "9")
37 foundNumber = 'Y';
38 else
39 sub += 1; //check the next character
40 }
41 //end while
42
43 //display message regarding numbers
44 if (foundNumber == 'N')
45 cout << ALL_NUMBERS << endl << endl;
46 else
47 cout << NOT_ALL_NUMBERS << endl << endl;
48 //end if
49 }
50 else
51 cout << INVALID_MSG << endl << endl;
52 //end if
53
54 cout << "Five-character ZIP code (-1 to end): ";
55 cin >> zipCode;
56 //end while
57
58 system("pause");
59 return 0;
60 //end of main function
```

You can use
sub++; in Line 38.

![](img/d64a28a68f49d61137bf2f3170ac40ad_562_0.png)

![](img/d64a28a68f49d61137bf2f3170ac40ad_562_1.png)

# The ZIP Code Program

```
Five-character ZIP code (-1 to end): 123
Invalid length

Five-character ZIP code (-1 to end): 12345
Valid length
All numbers

Five-character ZIP code (-1 to end): 123x4
Valid length
Not all numbers

Five-character ZIP code (-1 to end): -1
Press any key to continue . . 
```

13-19 Sample run of the modified ZIP code program

# Mini-Quiz 13-2

> The answers to Mini-Quiz questions are located in Appendix A.

- 1. Which of the following while clauses tells the computer to process the loop instructions as long as the employee contains more than 20 characters?
  a. while (employee.length() > 20)
  b. while (employee.length() > "20")
  c. while (employee.length() > '20');
  d. while (employee.length() > 20);
-2. Write a C++ if that determines whether a string named code contains seven characters.
3. The State variable contains the string "Los Angeles, CA". Which of the following assigns the state ID ("CA") to a string named state?
  a. state = cityState.substr(13);
  b. state = cityState.substr(13, 2);
  c. state = cityState.substr(14, 2);
  d. both a and b
4. Write a cout statement that displays the last character contained in the college variable. The variable has the string data type.

# The Rearranged Name Program

Figure 13-20 shows the problem specification and IPO chart for the rearranged name program. The program should allow the user to enter a person's first and last names, separated by a space. The program should display the person's last name followed by a comma, a space, and the person's first name. For example, if the user enters "Henry Smith", the program should display "Smith, Henry". As the indicates, you can accomplish this by searching for the space character that separates the first name from the last name. The characters to the left of the space character represent the first name. The characters to the right of the space character represent the last name.

Problem specification
Create a program that allows the user to enter a person's first and last names, separated by a space. The program should display the person's last name followed by a comma, a space, and the person's first name. For example, if the user enters "Henry Smith", the program should display "Smith, Henry".

| Input | Processing | Output |
| :--- | :--- | :--- |
| person's first and last names | 1. Enter the first and last names.<br>2. Search for the space character that separates them.<br>3. Assign the characters to the left of the space to the first name.<br>4. Assign the characters to the right of the space to the last name.<br>5. Display the last name followed by a comma, a space, and the first name. | rearranged name |

Algorithm:
1. enter the name
2. search for the space
3. assign the characters to the left of the space as the first name
4. assign the characters to the right of the space as the last name
5. display the last name followed by a comma, a space, and the first name

Figure 13-20 Problem specification and IPO chart for the rearranged name

# Searching the Contents of a string

You can use the string class to determine whether it contains a sequence of characters. For example, you can use the function to determine whether a phone number contains an area code. Or, you can use it to determine whether a street name appears in an address. Figure 13-21 shows the syntax of the find function.

## The find Function
string.find(searchString, subscript)

In the syntax, string is the name you want to search, and searchString is the string for which you are searching. The subscript argument is the index of the character at which to start the search.

```cpp
Example 1
int location = 0;
phone = "(312)9999";
location = phone.find("312", 0);
searches the phone variable, starting with the first character (subscript 0), to determine the location of the string "312"; stores the result (0) in the location variable
```

```cpp
Example 2
int spaceLocation = 0;
name = "Carol Cho";
spaceLocation = name.find(" ", 1);
searches the name variable, starting with the second character (subscript 1), to determine the location of the space character; stores the result (5) in the spaceLocation variable
```

```cpp
Example 3
int location = 0;
address = "210 Elm Street, Elmwood, NJ";
location = address.find("Elm ", 2);
searches the address variable, starting with the third character (subscript 2), to determine the location of the string "Elm"; stores the result (4) in the location variable
```

```cpp
Example 4
int location = 0;
address = "210 Elm Street, Elmwood, NJ";
location = address.find("elm ", 0);
searches the address variable, starting with the first character (subscript 0), to determine the location of the string "elm"; stores the result (-1) in the location variable
```

```cpp
Example 5
int location = 0;
address = "210 Elm Street, Elmwood, NJ";
location = address.find("Elm ", 9);
searches the address variable, starting with the tenth character (subscript 9), to determine the location of the string "Elm"; stores the result (-1) in the location variable
```

Notice the space after the letter m in the function in Examples 3, 4, and 5 in Figure 13-21.

Figure 13-21 How to use the find function (continued)

# The Rearranged Name Program

Figure 13-22 shows the code for the rearranged program. The find appears on Line 23 and is shaded in the figure. After the find function determines the location of the space, the program uses the two subst functions to separate the first name from the last name. The substr functions on Lines 24 and 25 and are shaded in the figure. Figure 13-23 shows a sample run of the program.

```cpp
//Rearranged Name.cpp
//Displays the last name followed by a comma,
// a space, and the first name
//Created/revised by <your name> on <current date>
5
#include <iostream>
#include <string>
```

Figure 13-22 Rearranged program name
