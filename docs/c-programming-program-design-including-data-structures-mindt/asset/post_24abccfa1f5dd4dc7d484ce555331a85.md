
```cpp
int *p2;
double *p3;
```

### 2.

Mark the following statements as valid or invalid. If a statement is invalid, explain why. (2, 3)

- a. `p1 = &num1;`
- b. `num2 = num1 - *p2;`
- c. `p3 = p2;`
- d. `*p3 = num1;`
- e. `*p3 = *p1;`
- f. `num1 = p2;`
- g. `p1 = &p2;`
- h. `p3 = &num1;`
- i. `num1 = *p3;`
- j. `num2 = &p1;`

### 3.

How is `*` used to create pointers? Give an example to justify your answer. (2)

- b. How is `*` used to dereference pointers? Give an example to justify your answer. (2)

### 4.

Consider the following statement:

```cpp
int* p, q;
```

This statement could lead to what type of misinterpretation? (2)

### 5.

Suppose that you have the declaration `int *numPtr;`. What is the difference between the expressions `*numPtr` and `&numPtr`? (3)

### 6.

What is the output of the following C++ code? (2, 3)

```cpp
int int1 = 26;
int int2 = 45;
int *int1Ptr = &int1;
int *int2Ptr = &int2;

*int1Ptr = 89;
*int2Ptr = 62;
int1Ptr = int2Ptr;
*int1Ptr = 80;
int1 = 57;

cout << int1 << " " << int2 << endl;
cout << *int1Ptr << " " << *int2Ptr << endl;
```

### 7.

Given the following statements:

```cpp
int num;
int *numPtr;
```

write C++ statements that use the variable `numPtr` to increment the value of the variable `num`. (2, 3)

```cpp
cout << "Radius of the base: " << baseRadius << endl;
cout << "Height: " << height << endl;
cout << "Volume: " << 3.14 * (baseRadius) * (baseRadius)
     << endl;
cout << "Surface area: "
     << 2 * 3.14 * (baseRadius) * (height) << endl;
```

### 11.

The following code is intended to find the area and perimeter of a rectangle. However, it fails to do so. Provide the correct code to accomplish the desired result. Also, do not modify the numerical values assigned to the variables in the code. After correcting the code, what is the output? (2, 3, 6)

```cpp
double *length;
double *width;

cout << fixed << showpoint << setprecision(2);

length = new double;
length = 6.5;

&width = 3.0;

cout << "Area: " << (*length) * (&width) << ", ";
cout << "Perimeter: " << 2 * (*length + width) << endl;
```

### 12.

What is the output of the following C++ code? (2, 3, 6)

```cpp
int *myPtr = new int;
int *yourPtr = new int;

*myPtr = 10;
*yourPtr = 2 * *myPtr + 3;
cout << *myPtr << " " << (*yourPtr - *myPtr + 5) << endl;

yourPtr = myPtr;
myPtr = new int;
*yourPtr = 8;
cout << *myPtr << " " << *yourPtr << endl;

*myPtr = 17;
*yourPtr = 4;

cout << *myPtr << " " << *yourPtr << endl;
```

### 13.

What is the output of the following C++ code? (2, 3, 6)

```cpp
double *trip1Cost = new double;
double *trip2Cost = new double;
double *trip3Cost = new double;
double *max;

*trip1Cost = 100.00;
*trip2Cost = 350.00;
*trip3Cost = trip2Cost;

trip2Cost = trip1Cost;
trip1Cost = new double;
*trip1Cost = 175;
*trip3Cost = 275;

cout << fixed << showpoint << setprecision(2);

cout << "Trip total cost: $"
     << (*trip1Cost + *trip2Cost + *trip3Cost) << endl;

max = trip1Cost;
if (*max < *trip2Cost)
    max = trip2Cost;

if (*max < *trip3Cost)
    max = trip3Cost;

cout << "Highest trip cost: $" << *max << endl;
```

### 14.

The following code has syntax errors. Provide the correct code and the output. (2, 3, 6)

```cpp
    int *speed = new int;                         //Line 1
    double *travelTime;                            //Line 2
    double *distance;                              //Line 3

    *speed = 65;                                   //Line 4
    *travelTime = 8.5;                             //Line 5

    distance = new double;                        //Line 6

    distance = (*speed) * (*travelTime;            //Line 7

    cout << *distance << endl;                     //Line 8
```

### 15.

What is wrong with the following code? (2, 3, 6)

```cpp
    double *firstPtr = new double;                //Line 1
    double *nextPtr = new double;                 //Line 2

    *firstPtr = 62;                               //Line 3
    nextPtr = firstPtr;                            //Line 4
    delete firstPtr;                               //Line 5
    delete nextPtr;                                //Line 6
    firstPtr = new double;                         //Line 7
    *firstPtr = 28;                                //Line 8

    cout << *firstPtr << " " << *nextPtr << endl;  //Line 9
```

### 16.

What is the output of the following code? (2, 3, 6)

```cpp
    int *myPtr = new int;
    int *yourPtr;

    *myPtr = 15;
    yourPtr = new int;
delete myPtr;
myPtr = yourPtr;
*yourPtr = 28;
myPtr = new int;
*myPtr = 49;
*yourPtr = 34;
delete yourPtr;
yourPtr = myPtr;
myPtr = new int;
*myPtr = 54;

cout << *myPtr << " " << *yourPtr << endl;
```

### 17.

What is stored in numList after the following code executes? (8)

```cpp
int numList[6] = {25, 37, 62, 78, 92, 13};
int *listPtr = numList;
int *temp = listPtr + 2;
int num;

*listPtr = *(listPtr + 1) - *listPtr;
listPtr++;
num = *temp;
temp++;
listPtr++;
*listPtr = *temp;
*temp = num;
listPtr = listPtr + 2;
*listPtr = *(listPtr - 1);
```

### 18.

What is the output of the following code: (8)

```cpp
int *intArrayPtr;
int *temp;
intArrayPtr = new int[5];
*intArrayPtr = 7;
temp = intArrayPtr;

for (int i = 1; i < 5; i++)
{
    intArrayPtr++;
    *intArrayPtr = *(intArrayPtr - 1) + 2 * i;
}

intArrayPtr = temp;
for (int i = 0; i < 5; i++)
{
    cout << *intArrayPtr << " ";
    intArrayPtr++;
}

cout << endl;
```

### 19.

Suppose that numPtr is a pointer of type int and gpaPtr is a pointer of type double. Further suppose that numPtr = 1050 and gpaPtr = 2000. Also suppose that the size of the memory allocated for an `int` value is 4 bytes and the size of the memory allocated for a `double` value is 8 bytes. What are the values of `numPtr` and `gpaPtr` after the statements `numPtr = numPtr + 2;` and `gpaPtr = gpaPtr + 3;` execute? (7)

### 20.

What does the operator `new` do? (6)

### 21.

What does the operator `delete` do? (6)

### 22.

Assume that the input is: `10 7 20 40 60`. What is the output of the following code? (8)

```cpp
int *intList;

intList = new int[5];

for (int i = 0; i < 5; i++)
    cin >> intList[i];

for (int i = 4; i > 0; i--)
    intList[i] = intList[i] + intList[i - 1];

int sum = 0;
for (int i = 0; i < 5; i++)
{
    cout << intList[i] << " ";
    sum = sum + intList[i];
}

cout << endl << "Sum = " << sum << endl;
```

### 23.

Consider the following statement. (8)

```cpp
double *sales;
```

- a. Write the C++ statement that dynamically creates an array of 50 components of type `double` and assigns the base address of the array to `sales`.
- b. Write a C++ code that inputs data into the array `sales` from the standard input device.
- c. Write a C++ code that finds the index of the largest entry in the array `sales`.
- d. Write a C++ statement that deallocates the memory space of array to which `sales` points.

### 24.

Consider the following C++ code. (6, 8)

```cpp
string seasons[4] = {"Winter", "Spring", "Summer", "Fall"};
string *strPtr;
strPtr = new string[5];
for (int i = 0; i < 4; i++)
    strPtr[i] = seasons[i];
```

- a. Write a C++ code that outputs the contents of the array to which `strPtr` points.
- b. Write the C++ statement that deallocates the memory space occupied by the array to which `strPtr` points.

### 25.

Explain why you cannot use a range-based for loop on dynamic arrays. (9)

### 26.

What is wrong with the following code? (9)

```cpp
double *p;                 //Line 1

p = new double[5];         //Line 2

for (int i = 0; i < 5; i++)    //Line 3
    p[i] = pow(i, 2.0);        //Line 4

for (auto x: p)             //Line 5
    cout << x << " ";       //Line 6

cout << endl;               //Line 7
```

### 27.

Explain the difference between a shallow copy and a deep copy of data. (11)

### 28.

In the C++ code given in (a) and (b), find any syntax or logical errors. (8, 11)

```cpp
a.  int *myPtr = new int;             //Line 1
    int *yourPtr;                    //Line 2

    *myPtr = 5;                       //Line 3
    yourPtr = myPtr;                  //Line 4
    cout << *yourPtr << endl;         //Line 5
    delete yourPtr;                   //Line 6
    cout << *myPtr << endl;           //Line 7
```

```cpp
b.  int *myListPtr = new int[10];     //Line 1
    int *yourListPtr;                 //Line 2

    for (int i = 0; i < 10; i++)      //Line 3
        myListPtr[i] = i * (i - 1);   //Line 4

    yourListPtr = myListPtr;          //Line 5

    delete [] yourListPtr;            //Line 6

    for (int i = 0; i < 10; i++)      //Line 7
        cout << myListPtr[1] << " "; //Line 8

        cout << endl;                 //Line 9
```

### 29.

In the following code both myList and yourList are dynamic arrays of the same size. The code initializes the array myList to certain values. The value in each element of yourList should be twice the value in the corresponding element in myList. However, the output of this code would show that is not the case. Provide the correct code to accomplish the desired results. (8, 11)

```cpp
int *myList;
int *yourList;

myList = new int[5];
myList[0] = 8;
```
