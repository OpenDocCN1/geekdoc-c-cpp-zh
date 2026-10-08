# CHAPTER 13 Strings

```
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
13 {
14 const string VALID_MSG = "Valid length";
15 const string INVALID_MSG = "Invalid length";
16 const string ALL_NUMBERS = "All numbers";
17 const string NOT_ALL_NUMBERS = "Not all numbers";
18 string zipCode
19 char foundNumber
20 = "N";
21
22 cout << "Five-character ZIP code (-1 to end)": ";
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
33 while (sub < zipCode.length())
34 && foundNumber == 'N') {
35 if (zipCode.substr(sub, 1) >= "0" &&
36 //zipCode.substr(sub, 1) <= "9")
37 foundNumber = 'Y';
3
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
54 cout << "Five-character ZIP code (-1 to end)": ";
55 cin >> zipCode;
56 //end while
57
58 system("pause");
59 return 0;
60 //end of main function
```

You can use
sub++; in Line
38.

![](bbox=[0.313, 0.946, 0.563, 0.959])

![](bbox=[0.638, 0.887, 0.775, 0.922])

542