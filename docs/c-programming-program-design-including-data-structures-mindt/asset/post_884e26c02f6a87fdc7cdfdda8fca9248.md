
```cpp
cout << "Line 26: Inside funOne: a = " << a
     << ", b = " << b << ", v = " << v
     << ", and one = " << one << endl;        //Line 26
}
                                                //Line 27
void funTwo(int& x, int y, char& w)             //Line 28
{
    x++;                                        //Line 29
    y = y * 2;                                   //Line 30
    w = 'G';                                     //Line 31
                                                //Line 32
    cout << "Line 33: Inside funTwo: x = " << x
         << ", y = " << y << ", and w = " << w
         << endl;                               //Line 33
}                                               //Line 34
```

## Sample Run

```text
Line 12: Inside main: num1 = 10, num2 = 15, and ch = A
Line 26: Inside funOne: a = 11, b = 30, v = B, and one = 10
Line 14: After funOne: num1 = 10, num2 = 30, and ch = A
Line 33: Inside funTwo: x = 31, y = 50, and w = G
Line 16: After funTwo: num1 = 10, num2 = 31, and ch = G
```

Let us walk through this program. The values of the variables are shown before and/or after each statement executes.

Just before the statement in Line 9 executes, memory is allocated only for the variables of the function main; this memory is not initialized. After the statement in Line 11 executes, the variables are as shown in Figure 6-9.

![](img/b217c421655b51e7494cf3b89bb5432d_441_0.png)

**FIGURE 6-9** Values of the variables after the statement in Line 11 executes

The statement in Line 12 produces the following output:

```text
Line 12: Inside main: num1 = 10, num2 = 15, and ch = A
```

The statement in Line 13 is a function call to the function funOne. Now function funOne has three parameters (a, b, and v) and one local variable (one). Memory for the parameters and the local variable of the function funOne is allocated. Because the formal parameter b is a reference parameter, it receives the address (memory location) of the corresponding actual parameter, which is num2. The other two formal parameters are value parameters, so they copy the values of their corresponding actual parameters. Just before the statement in Line 22 executes, the variables are as shown in Figure 6-10.

![](img/b217c421655b51e7494cf3b89bb5432d_442_0.png)

**FIGURE 6-10** Values of the variables just before the statement in Line 22 executes

The following shows how the variables are manipulated after each statement from Lines 22 to 25 executes.

| St. # in Line | Value of the Variables | Statement and Effect |
|---|---|---|
| 22 | **main**: `num1 = 10`, `num2 = 15`, `ch = 'A'`<br>**funOne**: `a = 10`, `b` references `num2`, `v = 'A'`, `one = 10` | `one = a;`<br>Copy the value of `a` into `one`. |
| 23 | **main**: `num1 = 10`, `num2 = 15`, `ch = 'A'`<br>**funOne**: `a = 11`, `b` references `num2`, `v = 'A'`, `one = 10` | `a++;`<br>Increment the value of `a` by 1. |
| 24 | **main**: `num1 = 10`, `num2 = 30`, `ch = 'A'`<br>**funOne**: `a = 11`, `b` references `num2`, `v = 'A'`, `one = 10` | `b = b * 2;`<br>Multiply the value of `b` by 2 and store the result in `b`. Because `b` is the reference parameter and contains the address of `num2`, the value of `num2` is updated. |
| 25 | **main**: `num1 = 10`, `num2 = 30`, `ch = 'A'`<br>**funOne**: `a = 11`, `b` references `num2`, `v = 'B'`, `one = 10` | `v = 'B';`<br>Store `'B'` into `v`. |

The statement in Line 26 produces the following output:

**Line 26: Inside funOne: a = 11, b = 30, v = B, and one = 10**

After the statement in Line 26 executes, control goes back to Line 14 in main and the memory allocated for the variables of function funOne is deallocated. Figure 6-11 shows the values of the variables of the function main.

![](img/b217c421655b51e7494cf3b89bb5432d_443_0.png)

**FIGURE 6-11** Values of the variables after the statement in Line 14

Line 14 produces the following output:

**Line 14: After funOne: num1 = 10, num2 = 30, and ch = A**

The statement in Line 15 is a function call to the function funTwo. Now funTwo has three parameters: x, y, and w. Also, x and w are reference parameters, and y is a value parameter. Thus, x receives the address of its corresponding actual parameter, which is num2, and w receives the address of its corresponding actual parameter, which is ch. The variable y copies the value 25 into its memory cell. Figure 6-12 shows the values before the statement in Line 30 executes.

![](img/b217c421655b51e7494cf3b89bb5432d_443_1.png)

**FIGURE 6-12** Values of the variables before the statement in Line 30 executes

The following shows how the variables are manipulated after each statement from Lines 30 to 32 executes.

| St. # in Line | Value of the Variables | Statement and Effect |
|---|---|---|
| 30 | **main**: `num1 = 10`, `num2 = 31`, `ch = 'A'`; **funTwo**: `x = 31`, `y = 25`, `w = 'A'` | `x++;` Increment the value of x by 1. Because x is the reference parameter and contains the address of `num2`, the value of `num2` is incremented by 1. |
| 31 | **main**: `num1 = 10`, `num2 = 31`, `ch = 'A'`; **funTwo**: `x = 31`, `y = 50`, `w = 'A'` | `y = y * 2;` Multiply the value of y by 2 and store the result in y. |
| 32 | **main**: `num1 = 10`, `num2 = 31`, `ch = 'G'`; **funTwo**: `x = 31`, `y = 50`, `w = 'G'` | `w = 'G';` Store 'G' in w. Because w is the reference parameter and contains the address of ch, the value of ch is updated. |

Line 33 produces the following output:

```text
Line 33: Inside funTwo: x = 31, y = 50, and w = G
```

After the statement in Line 33 executes, control goes to Line 16. The memory allocated for the variables of function funTwo is deallocated. The values of the variables of function main are as shown in Figure 6-13.

![](img/b217c421655b51e7494cf3b89bb5432d_444_0.png)

**FIGURE 6-13** Values of the variables after the statement in Line 16

The statement in Line 16 produces the following output:

```text
Line 16: After funTwo: num1 = 10, num2 = 31, and ch = G
```

After the statement in Line 16 executes, the program terminates.

## EXAMPLE 6-15

This example also shows how reference parameters manipulate actual parameters.

```cpp
//Example 6-15: Reference and value parameters.
//Program: Makes you think.

#include <iostream>                                      //line 1

using namespace std;                                     //line 2

void addFirst(int& first, int& second);                  //line 3
void doubleFirst(int one, int two);                      //line 4
void squareFirst(int& ref, int val);                     //line 5

int main()                                               //line 6
{
    int num = 5;                                         //line 8

    cout << "Line 9: Inside main: num = " << num
         << endl;                                        //line 9

    addFirst(num, num);                                  //line 10
    cout << "Line 11: Inside main after addFirst:"
         << " num = " << num << endl;                   //line 11

    doubleFirst(num, num);                               //line 12
    cout << "Line 13: Inside main after "
         << "doubleFirst: num = " << num << endl;       //line 13

    squareFirst(num, num);                               //line 14
    cout << "Line 15: Inside main after "
         << "squareFirst: num = " << num << endl;       //line 15

    return 0;                                            //line 16
}                                                       //line 17

void addFirst(int& first, int& second)                   //line 18
{                                                       //line 19
    cout << "Line 20: Inside addFirst: first = "
         << first << ", second = " << second << endl;   //line 20

    first = first + 2;                                   //line 21

    cout << "Line 22: Inside addFirst: first = "
         << first << ", second = " << second << endl;   //line 22

    second = second * 2;                                 //line 23

    cout << "Line 24: Inside addFirst: first = "
         << first << ", second = " << second << endl;   //line 24
}                                                       //line 25
```
