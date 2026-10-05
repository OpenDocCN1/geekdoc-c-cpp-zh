# 454 CHAPTER 10 Pointers and Dynamic Arrays

Display 10.11 Member Function Definitions for PFArrayD Class (part 2 of 2)

```
40 PFArrayD& PFArrayD::operator = (const PFArrayD& rightSide)
41 {
42     if (capacity != rightSide.capacity) {
43         delete a;
44         a = new double[rightSide.capacity];
45     }
46 }
47 capacity = rightSide.capacity;
48 used = rightSide.used;
49 for (int i = 0; i < used; i++)
50     a[i] = rightSide.a[i];
51
52 return true;
```

> *Note that this also checks for the case of having the same object on both sides of the assignment operator.*

```
53 PFArrayD::~PFArrayD()
54 {
55     delete [];
56 }
57
```

Display 10.12 Demonstration Program for PFArrayD (part 1 of 2)

```
1 //Program to demonstrate the class PFArrayD
2 #include <iostream>
3 using namespace std;

4 class PFArrayD
5 {
6     <The rest of the class definition is the same as in Display 10.10.>
7 };

8 void testPFArrayD();
9 //Connects one test of the class PFArrayD.

10 int main()
11 {
12     cout << "This program tests the class PFArrayD.\n";
13     char ans;
14     do
15     {
16         testPFArrayD();
17         cout << "Test again? (y/n) ";
18         cin >> ans;
19     } while ((ans == 'y') || (ans == 'Y'));

20     return 0;
21 }
```

> In Section 11.1 of Chapter 11 we show how to divide this long file into three shorter files corresponding roughly to Displays 10.10, 10.11, and this display without the code from Displays 10.10 and 10.11.

![](bbox=[0.535, 0.968, 0.575, 0.983])