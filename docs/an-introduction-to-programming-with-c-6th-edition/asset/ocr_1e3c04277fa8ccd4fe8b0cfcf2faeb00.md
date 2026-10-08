# The ZIP Code Program

```
1 //ZIP Code.cpp
2 //Displays a message indicating whether a ZIP
3 //code's length is valid or invalid
4 //Created/revised by <name> on <current date>
5 
6 #include <iostream>
7 #include <string>
8 using namespace std;
9 int main()
10 {\n11     const string VALID_MSG = "Valid length"
12     const string INVALID_MSG = "Invalid length"
13     string zipCode = "";
14 
15     cout << "Five-character ZIP code (-1 to end): ";
16     cin >> zipCode;
17 
18     while (zipCode != "-1")
19     {
20         if (zipCode.length() == 5)
21             cout << VALID_MSG << endl;
22         else
23             cout << INVALID_MSG << endl;
24         //end if
25     }
26 
27     cout << "-Five-character ZIP code (-1 to end): ";
28     cout << zipCode;
29 } //end while
30 
31     system("pause");
32     return 0;
33 } //end of main function
```

Figure 13-14 ZIP code program

![](bbox=[0.118, 0.663, 0.663, 0.839])

Figure 13-15 Sample run of the ZIP code program