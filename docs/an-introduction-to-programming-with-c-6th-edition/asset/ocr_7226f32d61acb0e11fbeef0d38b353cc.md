# CHAPTER 12 Two-Dimensional Arrays

```
1 //Modified Caldwell Company.cpp
2 //Displays the contents of a two-dimensional array
3 //Created/revised by <your name> on <current date>
4
5 #include <iostream>
6 using namespace std;
7
8 //function prototype
9 void displayArray(int nums nums[4][3]);
10
11 int main()
12 {
13 //declare and initialize array
14 int orders[4][3] = {};
15
16 //enter data into the array
17 for (int region = 0; region < 4; region += 1)
18     for (int month = 0; month < 3; month += 1)
19         {
20             cout << "Number of orders for Region "
21                 << region + 1 << ", "
22                 << month + 1 << ": ";
23             cin >> orders[region][month];
24         }
25 //end for
26
27 //display the contents of the array
28 displayArray(orders);
29
30 system("pause");
31 return 0;
32 //end of main function
33 void displayArray(int nums[4][3]) {
34 for (int region = 0; region < 4; region += 1)
35     {
36         cout << "Region " << region + 1
37             << ": " << endl;
38         for (int month = 0; month < 3; month += 1)
39             {
40                 cout << "Month " << month + 1
41                 << ": " " << nums[region][month] << endl;
42             }
43         } //end for
44 }
45 //end of displayArray function
```

You can use region++ in Lines 17, and 37, and month++ in Lines 18 and 41.

> your C++ development tool may not require this statement

Figure-12 Modified Caldwell Company orders program