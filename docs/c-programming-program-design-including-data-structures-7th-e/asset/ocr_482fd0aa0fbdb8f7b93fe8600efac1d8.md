```
```cpp
*p = 32;
*q = 20;
cout << 2 * (*p) << " " << (*q - 5) << endl;
q = p;
*p = 10;
cout << *p << " " << *q << endl;
p = new int;
*p = 12;
*q = 62;
cout << *p << " " << *q << endl;
```
```

13. What is the output of the following C++ code? (Assume that decimal numbers are output with two decimal places.) (2, 3, 6)

```
```cpp
double *test1 = new double;
double *test2 = new double;
double *average;
average = test1;
*test1 = 45.00;
*test2 = 90.00;
test1 = test2;
test2 = new double;
*test2 = 86.00;
*average = ((*test1) + (*test2)) / 2;
cout << *test1 << " " << *test2 << " " << *average << endl;
```
```

14. What is wrong with the following C++ code? (2, 3, 6)

```
```cpp
double *deposit; //Line 1
double *intRate; //Line 2
double interest; //Line 3

deposit = new double; //Line 4
*deposit = 25000; //Line 5

interest = (*deposit) * (*intRate); //Line 6

cout << interest << endl; //Line 7
```
```

15. What is wrong with the following C++ code? (2, 3, 6)

```
```cpp
double *firstPtr = new double; //Line 1
double *nextPtr = new double; //Line 2

*firstPtr = 62; //Line 3
nextPtr = firstPtr; //Line 4
delete firstPtr; //Line 5
delete nextPtr; //Line 6
firstPtr = new double; //Line 7
*firstPtr = 28; //Line 8

cout << *firstPtr << " " << *nextPtr << endl; //Line 9
```
```

16. What is the output of the following C++ code? (2, 3, 6)

```
```cpp
int *p;
int *q = new int;
```
```