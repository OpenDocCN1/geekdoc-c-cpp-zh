# Display 4.8 Default Arguments

```
1
2 #include <iostream>
3 using namespace std;
4 void showVolume(int length, int width = 1, int height = 1);
5 //Returns the volume of a box.
6 //If no height is given, the height is assumed to be 1.
7 //If neither height nor width is given, both are assumed to be 1.
8 int main()
9 {
10     showVolume(4, 6, 2);
11     showVolume(4, 6);
12     showVolume(4);
13     return 0;
14 }
15 void showVolume(int length, int width, int height)
16 {
17     cout << "Volume of a box with \n"
18     << "Length = " << length << ", Width = " << width << endl
19     << "and Height = " << height
20     << " is " << length*width*height << endl;
21 }
```

> Default arguments

> A default argument should not be given a second time.

# Sample Dialogue

```
Volume of a box with
Length = 4, Width = 6
and Height = 2 is 48
Volume of a box with
Length = 4, Width = 6
and Height = 1 is 24
Volume of a box with
Length = 4, Width = 1
and Height = 1 is 4
```

# Self-Test Exercise

10. This question has to do with the programming example entitled "Revised Pizza-Buying Program." Suppose the evil pizza parlor that is always trying to fool customers introduces a square pizza. Can you overload the function unitPrice so that it can compute the price per square inch of a square pizza as well as the price per square inch of a round pizza? Why or why not?