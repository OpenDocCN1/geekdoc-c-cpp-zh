# // QUIZ ANSWERS

+   1 a bool

+   b 0

+   c 1

+   d true (remember: any nonzero value is treated as true)

+   4 Output 3

Notice that because the first conditional (a==b) is false (a is 3 and b is 4, so they are not equal, and the comparison is false), the else clause is followed. The next step is for the nested conditional to check whether b is not equal to c (b!=c). b is 4 and c is 3, they are not equal, so the comparison is true. So, the first clause is followed, and the line Output 3 is output.

+   2 a !=

+   b ==

+   c !

+   d &&&

+   e ||

+   5 There are multiple possible answers. Here is one:

+   3 true:

```
!((true && true) || (false && true)) || (!true) || (!false && true))
!(( true || false) || (false || ( true && true ))
!(false || ( false || ( true ))
false || true
```

```
1 // Report phase<iostream>
2 using namespace std;
3
4 int main() {
5 float temperature;
6 cout << "Enter a temperature in
7 Fahrenheit: ";
8
9 cin >> temperature;
10 if (temperature == 32) {
11 cout << "Ice" << endl;
12 else if (temperature == 32) {
13 cout << "Freezing" << endl;
14 else if (temperature == 212) {
15 cout << "Liquid" << endl;
16 else if (temperature == 212) {
17 cout << "Boiling" << endl;
18 else {
19 cout << "Vapor" << endl;
20 }
```