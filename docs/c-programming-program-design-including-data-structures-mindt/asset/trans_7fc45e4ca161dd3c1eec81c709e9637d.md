

```cpp
int *p2;
double *p3;
```

### 2.

将下列语句标记为有效或无效。如果语句无效，请解释原因。(2, 3)

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

`*` 如何用于创建指针？请举例说明你的答案。(2)

- b. `*` 如何用于解引用指针？请举例说明你的答案。(2)

### 4.

考虑以下语句：

```cpp
int* p, q;
```

该语句可能导致哪种类型的误解？(2)

### 5.

假设你有声明 `int *numPtr;`。表达式 `*numPtr` 和 `&numPtr` 之间有什么区别？(3)

### 6.

以下 C++ 代码的输出是什么？(2, 3)

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

给定以下语句：

```cpp
int num;
int *numPtr;
```

编写 C++ 语句，使用变量 `numPtr` 递增变量 `num` 的值。(2, 3)

```cpp
cout << "Radius of the base: " << baseRadius << endl;
cout << "Height: " << height << endl;
cout << "Volume: " << 3.14 * (baseRadius) * (baseRadius)
     << endl;
cout << "Surface area: "
     << 2 * 3.14 * (baseRadius) * (height) << endl;
```

### 11.

以下代码旨在求矩形的面积和周长。然而，它未能做到。提供正确的代码以实现预期结果。此外，不要修改代码中赋给变量的数值。修正代码后，输出是什么？(2, 3, 6)

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

以下 C++ 代码的输出是什么？(2, 3, 6)

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

以下 C++ 代码的输出是什么？(2, 3, 6)

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

以下代码存在语法错误。提供正确的代码和输出。(2, 3, 6)

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

以下代码有什么问题？(2, 3, 6)

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

以下代码的输出是什么？(2, 3, 6)

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

以下代码执行后，`numList` 中存储的是什么？(8)

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

以下代码的输出是什么：(8)

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

假设 `numPtr` 是 int 类型的指针，`gpaPtr` 是 double 类型的指针。进一步假设 `numPtr = 1050` 且 `gpaPtr = 2000`。还假设为 `int` 值分配的内存大小为 4 字节，为 `double` 值分配的内存大小为 8 字节。在语句 `numPtr = numPtr + 2;` 和 `gpaPtr = gpaPtr + 3;` 执行后，`numPtr` 和 `gpaPtr` 的值是什么？(7)

### 20.

运算符 `new` 做什么？(6)

### 21.

运算符 `delete` 做什么？(6)

### 22.

假设输入为：`10 7 20 40 60`。以下代码的输出是什么？(8)

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

考虑以下语句。(8)

```cpp
double *sales;
```

- a. 编写 C++ 语句，动态创建一个包含 50 个 `double` 类型分量的数组，并将该数组的基地址赋给 `sales`。
- b. 编写 C++ 代码，从标准输入设备将数据输入到数组 `sales` 中。
- c. 编写 C++ 代码，找出数组 `sales` 中最大元素的索引。
- d. 编写 C++ 语句，释放 `sales` 所指向数组的内存空间。

### 24.

考虑以下 C++ 代码。(6, 8)

```cpp
string seasons[4] = {"Winter", "Spring", "Summer", "Fall"};
string *strPtr;
strPtr = new string[5];
for (int i = 0; i < 4; i++)
    strPtr[i] = seasons[i];
```

- a. 编写 C++ 代码，输出 `strPtr` 所指向数组的内容。
- b. 编写 C++ 语句，释放 `strPtr` 所指向数组占用的内存空间。

### 25.

解释为什么不能对动态数组使用基于范围的 for 循环。(9)

### 26.

以下代码有什么问题？(9)

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

解释数据浅拷贝和深拷贝之间的区别。(11)

### 28.

在 (a) 和 (b) 给出的 C++ 代码中，找出任何语法或逻辑错误。(8, 11)

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

在以下代码中，`myList` 和 `yourList` 都是相同大小的动态数组。代码将数组 `myList` 初始化为某些值。`yourList` 中每个元素的值应为 `myList` 中对应元素值的两倍。然而，该代码的输出会表明并非如此。提供正确的代码以实现预期结果。(8, 11)

```cpp
int *myList;
int *yourList;

myList = new int[5];
myList[0] = 8;
```

