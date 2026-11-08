
After the statement in Line 9, `one = a;`, executes, the variables are as shown in Figure 6-11.

![](img/dc1b115c1ae2ec0d8a557b7c2b830e8c_422_0.png)

**FIGURE 6-11** Values of the variables after the statement in Line 9 executes

After the statement in Line 10, `a++;`, executes, the variables are as shown in Figure 6-12.

![](img/dc1b115c1ae2ec0d8a557b7c2b830e8c_422_1.png)

**FIGURE 6-12** Values of the variables after the statement in Line 10 executes

After the statement in Line 11, `b = b * 2;`, executes, the variables are as shown in Figure 6-13. (Note that the variable b changed the value of num2.)

![](img/dc1b115c1ae2ec0d8a557b7c2b830e8c_422_2.png)

**FIGURE 6-13** Values of the variables after the statement in Line 11 executes

After the statement in Line 12, `v = 'B'`, executes, the variables are as shown in Figure 6-14.

![](img/dc1b115c1ae2ec0d8a557b7c2b830e8c_423_0.png)

**FIGURE 6-14** Values of the variables after the statement in Line 12 executes

The statement in Line 13 produces the following output:

```text
Line 13: Inside funOne: a = 11, b = 30, v = B, and one = 10
```

After the statement in Line 13 executes, control goes back to Line 6 and the memory allocated for the variables of function funOne is deallocated. Figure 6-15 shows the values of the variables of the function main.

![](img/dc1b115c1ae2ec0d8a557b7c2b830e8c_423_1.png)

**FIGURE 6-15** Values of the variables when control goes back to Line 6

Line 6 produces the following output:

```text
Line 6: After funOne: num1 = 10, num2 = 30, and ch = A
```

The statement in Line 7 is a function call to the function funTwo. Now funTwo has three parameters: x, y, and w. Also, x and w are reference parameters, and y is a value parameter. Thus, x receives the address of its corresponding actual parameter, which is num2, and w receives the address of its corresponding actual parameter, which is ch. The variable y receives the value 25 into its memory cell. Figure 6-16 shows the values before the statement in Line 14 executes.

![](img/dc1b115c1ae2ec0d8a557b7c2b830e8c_424_0.png)

**FIGURE 6-16** Values of the variables before the statement in Line 14 executes

After the statement in Line 14, `x++`, executes, the variables are as shown in Figure 6-17. (Note that the variable `x` changed the value of `num2`.)

![](img/dc1b115c1ae2ec0d8a557b7c2b830e8c_424_1.png)

**FIGURE 6-17** Values of the variables after the statement in Line 14 executes

After the statement in Line 15, `y = y * 2`, executes, the variables are as shown in Figure 6-18.

![](img/dc1b115c1ae2ec0d8a557b7c2b830e8c_424_2.png)

**FIGURE 6-18** Values of the variables after the statement in Line 15 executes

After the statement in Line 16, `w = 'G'`, executes, the variables are as shown in Figure 6-19. (Note that the variable `w` changed the value of `ch`.)

![](img/dc1b115c1ae2ec0d8a557b7c2b830e8c_425_0.png)

Line 17 produces the following output:

```text
Line 17: Inside funTwo: x = 31, y = 50, and w = G
```

After the statement in Line 17 executes, control goes to Line 8. The memory allocated for the variables of function funTwo is deallocated. The values of the variables of the function main are as shown in Figure 6-20.

![](img/dc1b115c1ae2ec0d8a557b7c2b830e8c_425_1.png)

The statement in Line 8 produces the following output:

```text
Line 8: After funTwo: num1 = 10, num2 = 31, and ch = G
```

After the statement in Line 8 executes, the program terminates.

## EXAMPLE 6-14

This example also shows how reference parameters manipulate actual parameters.

```cpp
//Example 6-14: Reference and value parameters.
//Program: Makes you think.

#include <iostream>

using namespace std;

void addFirst(int& first, int& second);
void doubleFirst(int one, int two);
void squareFirst(int& ref, int val);

int main()
{
    int num = 5;

    cout << "Line 1: Inside main: num = " << num
         << endl;                                  //Line 1

    addFirst(num, num);                             //Line 2
    cout << "Line 3: Inside main after addFirst:"
         << " num = " << num << endl;              //Line 3

    doubleFirst(num, num);                          //Line 4
    cout << "Line 5: Inside main after "
         << "doubleFirst: num = " << num << endl;  //Line 5

    squareFirst(num, num);                          //Line 6
    cout << "Line 7: Inside main after "
         << "squareFirst: num = " << num << endl;  //Line 7

    return 0;
}

void addFirst(int& first, int& second)
{
    cout << "Line 8: Inside addFirst:  first = "
         << first << ", second = " << second << endl; //Line 8

    first = first + 2;                              //Line 9

    cout << "Line 10: Inside addFirst:  first = "
         << first << ", second = " << second << endl; //Line 10

    second = second * 2;                            //Line 11

    cout << "Line 12: Inside addFirst:  first = "
         << first << ", second = " << second << endl; //Line 12
}

void doubleFirst(int one, int two)
{
    cout << "Line 13: Inside doubleFirst:  one = "
         << one << ", two = " << two << endl;      //Line 13

    one = one * 2;                                  //Line 14

    cout << "Line 15: Inside doubleFirst: one = "
         << one << ", two = " << two << endl;      //Line 15

    two = two + 2;                                  //Line 16

    cout << "Line 17: Inside doubleFirst: one = "
         << one << ", two = " << two << endl;          //Line 17
}

void squareFirst(int& ref, int val)
{
    cout << "Line 18: Inside squareFirst: ref = "
         << ref << ", val = " << val << endl;       //Line 18

    ref = ref * ref;                                 //Line 19

    cout << "Line 20: Inside squareFirst: ref = "
         << ref << ", val = " << val << endl;       //Line 20

    val = val + 2;                                   //Line 21

    cout << "Line 22: Inside squareFirst: ref = "
         << ref << ", val = " << val << endl;       //Line 22
}
```

### Sample Run:

```text
Line 1: Inside main:  num = 5
Line 8: Inside addFirst:  first = 5, second = 5
Line 10: Inside addFirst:  first = 7, second = 7
Line 12: Inside addFirst:  first = 14, second = 14
Line 3: Inside main after addFirst:  num = 14
Line 13: Inside doubleFirst: one = 14, two = 14
Line 15: Inside doubleFirst: one = 28, two = 14
Line 17: Inside doubleFirst: one = 28, two = 14
Line 5: Inside main after doubleFirst:  num = 14
Line 18: Inside squareFirst: ref = 14, val = 14
Line 20: Inside squareFirst: ref = 196, val = 14
Line 22: Inside squareFirst: ref = 196, val = 16
Line 7: Inside main after squareFirst:  num = 196
```

Both parameters of the function addFirst are reference parameters, and both parameters of the function doubleFirst are value parameters. The statement:

```cpp
addFirst(num, num);
```

in the function main (Line 2) passes the reference of num to both formal parameters first and second of the function addFirst, because the corresponding actual parameters for both formal parameters are the same. That is, the variables first and second refer to the same memory location, which is num. Figure 6-21 illustrates this situation.

![](img/dc1b115c1ae2ec0d8a557b7c2b830e8c_428_0.png)

**FIGURE 6-21** Parameters of the function `addFirst`

Any changes that first makes to its value immediately change the value of second and num. Similarly, any changes that second makes to its value immediately change first and num, because all three variables refer to the same memory location. (Note that num was initialized to 5.)

The formal parameters of the function `doubleFirst` are value parameters. So the statement:

```cpp
doubleFirst(num, num);
```

in the function `main` (Line 4) copies the value of `num` into one and two because the corresponding actual parameters for both formal parameters are the same. Figure 6-22 illustrates this scenario.

![](img/dc1b115c1ae2ec0d8a557b7c2b830e8c_428_1.png)

**FIGURE 6-22** Parameters of the function `doubleFirst`

Because both one and two are value parameters, any changes that one makes to its value do not affect the values of two and num. Similarly, any changes that two makes to its value do not affect one and num. (Note that the value of num before the function `doubleFirst` executes is 14.)

The formal parameter `ref` of the function `squareFirst` is a reference parameter, and the formal parameter `val` is a value parameter. The variable `ref` receives the address of its corresponding actual parameter, which is `num`, and the variable `val` copies the value of its corresponding actual parameter, which is also `num`. Thus, both `num` and `ref` refer to the same memory location, which is `num`. Figure 6-23 illustrates this situation.
