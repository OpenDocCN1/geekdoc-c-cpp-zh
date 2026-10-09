leap-year/LeapYear.cs

```
```
namespace Example;

delegate bool IsLeapYear(int year);
```
```

We will discuss "delegates" shortly.

Here's the first implementation:

leap-year/LeapYear1.cs

```
```
1 namespace Example;
2
3 static class LeapYear1 {
4 internal static bool IsLeapYear(int year) {
5 if (year % 4 == 0) {
6 if (year % 100 == 0) {
7 if (year % 400 == 0) {
8 return true;
9 } else {
10 return false;
11 }
12 } else {
13 return true;
14 }
15 } else {
16 return false;
17 }
18 }
19 }
```
```

The second implementation: