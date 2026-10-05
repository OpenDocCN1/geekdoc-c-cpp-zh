# Programming with Arrays

Display 5.5 Partially Filled Array (part 1 of 2)

+   1 //Shows the difference between each of a list of golf scores and
// their average.

```
2 #include <iostream>
3 using namespace std;
4 const int MAX_NUMBER_SCORES = 10;
```

```
5 void fillArray(int a[], int size, int& numberUsed)
6 //Precondition: size is the declared size of the array a.
7 //Postcondition: numberUsed is the number of values stored in a.
8 //a[0] through [numberUsed-1] have been filled with
//nonnegative integers from the keyboard.
```

```
10 double computeAverage(const int a[], int numberUsed)
11 //Precondition: a through [numberUsed-1] have values
//numberUsed > 0.
12 //Returns the average of numbers a[0] through [numberUsed-1].
```

```
13 void showDifference(const int a[], int numberUsed)
14 //Precondition: The first numberUsed indexed variables of a have values.
15 //Postcondition: Gives output showing how much each of the first
//nonnegative elements of the array differs from their average.
17 int main()
```

```
18 {
19 int score[MAX_NUMBER_SCORES], numberUsed;
20 cout << "This program reads golf scores and shows\n"
21 << "how much each differs from the average.\n";
```

```
23 cout << "Enter golf scores:\\n";
```

```
25 fillArray(score, MAX_NUMBER_SCORES, numberUsed)
26 showDifference(score, numberUsed);
```

```
27 return 0;
28 }
```

```
30 void fillArray(int a[], int size, int& numberUsed)
31 {
32 cout << "Enter up to " << size << " << nonnegative numbers.\\n"
33 << "Mark the end of the list with a negative number.\\n"
34 int next, index = 0;
35 cin >> next;
36 while ((next >= 0) && (index < size))
37 {
```

```
38 a[index] = next;
39 index++;
40 cin >> next;
41 }
```

(continued)