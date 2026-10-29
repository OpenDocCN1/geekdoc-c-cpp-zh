
## Figure 8.2 The variable num stored somewhere in memory

![](img/e9bf940282dfb289356f077151cc69dd_362_0.png)

C++ permits you to go further, however, and display the address corresponding to any variable. The address that's displayed corresponds to the address of the first byte set aside in the computer's memory for the variable.

To determine a variable's address, the address operator, &, must be used. You have seen this symbol before in declaring reference variables. When used to display an address, it means "the address of," and when placed in front of a variable name, it's translated as the address of the variable.² For example, &num means "the address of num," &total means "the address of total," and &price means "the address of price." Program 8.2 uses the address operator to display the address of the variable num.

## Program 8.2

```
#include <iostream>
using namespace std;

int main()
{
    int num;

    num = 22;
    cout << "The value stored in num is " << num << endl;
    cout << "The address of num = " << &num << endl;

    return 0;
}
```

This is the output of Program 8.2:

```
The value stored in num is 22
The address of num = 0012FED4
```

> ²When used in the declaration of a reference variable (see Section 6.3), the & symbol refers to the data type preceding it. For example, the declaration int &num is read as "num is the address of an int" or, more commonly, "num is a reference to an int."

Figure 8.3 shows the additional address information provided by Program 8.2’s output.

![](img/e9bf940282dfb289356f077151cc69dd_363_0.png)

Figure 8.3 A more complete picture of the variable num

Clearly, the address output by Program 8.2 depends on both the computer used to run the program and what other programs or data files are in memory when the program runs. Every time Program 8.2 runs, however, it displays the address of the first memory location used to store num. As Program 8.2’s output shows, the address is displayed in hexadecimal notation (see Section 2.6). This display has no effect on how the program uses addresses internally; it merely provides a means of displaying addresses in a more compact representation than the internal binary system used by the computer. As you see in the following sections, however, using addresses (as opposed to just displaying them) gives C++ programmers a powerful programming tool.

## Storing Addresses

Besides displaying the address of a variable, as in Program 8.2, you can store addresses in suitably declared variables. For example, the statement

```
numAddr = &num;
```

stores the address corresponding to the variable num in the variable numAddr, as illustrated in Figure 8.4.

![](img/e9bf940282dfb289356f077151cc69dd_363_1.png)

Figure 8.4 Storing num’s address in numAddr

Similarly, the statements

```
d = &m;
tabPoint = &list;
chrPoint = &ch;
```

store addresses of the variables m, list, and ch in the variables d, tabPoint, and chrPoint, as shown in Figure 8.5.

## Figure 8.5 Storing more addresses

| Variable | Contents |
|---|---|
| d | Address of m |
| tabPoint | Address of list |
| chrPoint | Address of ch |

The variables numAddr, d, tabPoint, and chrPoint are formally called pointer variables or pointers. Pointers are simply variables used to store the addresses of other variables.

## Using Addresses

To use a stored address, C++ provides an indirection operator, *. The * symbol, when followed by a pointer (with a space permitted both before and after the *), means "the variable whose address is stored in." Therefore, if numAddr is a pointer (a variable that stores an address), *numAddr means the variable whose address is stored in numAddr. Similarly, *tabPoint means the variable whose address is stored in tabPoint, and *chrPoint means the variable whose address is stored in chrPoint. Figure 8.6 shows the relationship between the address contained in a pointer variable and the variable.

## Figure 8.6 Using a pointer variable

A pointer variable y
The contents of y are an address
The contents at address mmmm are qqqq

Although *d means "the variable whose address is stored in d," it's commonly shortened to the statement "the variable pointed to by d." Similarly, referring to Figure 8.6, *y can be read as "the variable pointed to by y." The value that's finally obtained, as shown in this figure, is qqqq.

When using a pointer variable, the value that's finally obtained is always found by first going to the pointer for an address. The address contained in the pointer is then used to get the variable's contents. Certainly, this procedure is a rather indirect way of getting to the final value, so the term indirect addressing is used to describe it.

Because using a pointer requires the computer to do a double lookup (retrieving the address first, and then using the address to retrieve the actual data), you might wonder why you'd want to store an address in the first place. The answer lies in the shared relationship between pointers and arrays and the capability of pointers to create and delete variable storage locations dynamically, as a program is running. Both topics are discussed in the next section. For now, however, given that each variable has a memory address associated with it, the idea of storing an address shouldn't seem unusual.

## Declaring Pointers

Like all variables, pointers must be declared before they can be used to store an address. When you declare a pointer variable, C++ requires also specifying the type of variable that's pointed to. For example, if the address in the pointer numAddr is the address of an integer, this is the correct declaration for the pointer:

```
int *numAddr;
```

This declaration is read as "the variable pointed to by numAddr (from *numAddr in the declaration) is an integer."³

Notice that the declaration int *numAddr; specifies two things: First, the variable pointed to by numAddr is an integer, and second, numAddr must be a pointer (because it's declared with an asterisk, *). Similarly, if the pointer tabPoint points to (contains the address of) a double-precision number and chrPoint points to a character variable, the required declarations for these pointers are as follows:

```
double *tabPoint;
char *chrPoint;
```

These two declarations can be read as "the variable pointed to by tabPoint is a double" and "the variable pointed to by chrPoint is a char." Because all addresses appear the same, the compiler needs this additional information to know how many storage locations to access when it uses the address stored in the pointer.

Here are other examples of pointer declarations:

```
char *inkey;
int *numPt;
double *numPtr
```

To understand pointer declarations, reading them backward is helpful, starting with the asterisk, *, and translating it as "the variable whose address is stored in" or "the variable pointed to by." Applying this method to pointer declarations, the declaration char *inkey; for example, can be read as "the variable whose address is stored in inkey is a char" or "the variable pointed to by inkey is a char." Both these statements are often shortened to the simpler "inkey points to a char." All three interpretations of the declaration statement are correct, so you can select and use the description that makes the most sense to you. Program 8.3 puts this information together to construct a program using pointers.

## Program 8.3

```
#include <iostream>
using namespace std;

int main()
{
    int *numAddr;      // declare a pointer to an int
    int miles, dist;   // declare two integer variables

    dist = 158;        // store the number 158 in dist
    miles = 22;        // store the number 22 in miles
    numAddr = &miles;  // store the "address of miles" in numAddr

    cout << "The address stored in numAddr is " << numAddr << endl;
    cout << "The value pointed to by numAddr is " << *numAddr << "\n\n";

    numAddr = &dist; // now store the address of dist in numAddr
    cout << "The address now stored in numAddr is " << numAddr << endl;
    cout << "The value now pointed to by numAddr is " << *numAddr << endl;

    return 0;
}
```

The output of Program 8.3 is as follows:

```
The address stored in numAddr is 0012FEC8
The value pointed to by numAddr is 22

The address now stored in numAddr is 0012FEBC
The value now pointed to by numAddr is 158
```

The only use for Program 8.3 is to help you understand what gets stored where, so review the program to see how the output was produced. The declaration statement int *numAddr; declares numAddr to be a pointer used to store the address of an integer variable. The statement numAddr = &miles; stores the address of the variable miles in the pointer numAddr. The first cout statement causes this address to be displayed. The second cout statement uses the indirection operator (*) to retrieve and display the value pointed to by numAddr, which is, of course, the value stored in miles.

Because numAddr has been declared as a pointer to an integer variable, you can use this pointer to store the address of any integer variable. The statement numAddr = &dist illustrates this use by storing the address of the variable dist in numAddr. The last two cout statements verify the change in numAddr's value and confirm that the new stored address points to the variable dist. As shown in Program 8.3, only addresses should be stored in pointers.
