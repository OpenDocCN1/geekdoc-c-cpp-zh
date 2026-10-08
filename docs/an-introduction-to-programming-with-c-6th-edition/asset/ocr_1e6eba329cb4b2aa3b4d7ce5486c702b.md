# CHAPTER 13 Strings

using the length function. The cout statement in Example 1 uses the length function to display the number of characters (15) contained in the name variable. The if clause in Example 2 uses the length function to compare the number of characters stored in the zipCode variable with the number 5. The while clause in Example 3 uses the length function to repeat the loop as long as the partNum variable does not contain exactly six characters.

536

# HOW TO Use the length Function
Syntax
string.length()

Example 1
string name = "Nancy Haberdeen";
out << name.length() << endl;
displays the number 15 on the screen

Example 2
const string VALID_MSG = "Valid length";
const string INVALID_MSG = "Invalid length";
string zipCode = "";
out << "Five-character ZIP code: " <<;
cin >> zipCode;
if (zipCode.length() == 5)
cout << VALID_MSG << endl;
elelse
cout << INVALID_MSG << endl;
//end if.
compares the number of characters stored in the zipCode variable with the
number 5 and then displays an appropriate message

Example 3
string partNum = "";
out << "Six-character part number: " <<;;
getline(cin, partNum);
while (partNum.length() != 6)
{
cout << "Six-character part number: " <<;;
getline(cin, partNum);
}
//end while
continues gets part number until the user enters exactly six characters

Figure 13-13 How to use the length function

Figure 13-14 shows the ZIP code program. The length function appears in
t if clause on Line 21 and is shaded in the figure. Figure 13-15 shows a
sample run of the program.