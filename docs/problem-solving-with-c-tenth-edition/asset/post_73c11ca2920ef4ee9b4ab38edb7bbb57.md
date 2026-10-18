
- The indexed variables for an array are stored next to each other in the computer’s memory so that the array occupies a contiguous portion of memory. When the array is passed as an argument to a function, only the address of the first indexed variable (the one numbered 0) is given to the calling function. Therefore, a function with an array parameter usually needs another formal parameter of type `int` to give the size of the array.

- When using a partially filled array, your program needs an additional variable of type `int` to keep track of how much of the array is being used.

- To tell the compiler that an array argument should not be changed by your function, you can insert the modifier `const` before the array parameter for that argument position. An array parameter that is modified with a `const` is called a **constant array parameter**.

- If you need an array with more than one index, you can use a multidimensional array, which is actually an array of arrays.

## Answers to Self-Test Exercises

**1.** The statement `int a[5];` is a declaration, where 5 is the number of array elements. The expression `a[4]` is an access into the array defined by the previous statement. The access is to the element having index 4, which is the fifth (and last) array element.

**2.** a. `score`  
b. `double`  
c. 5  
d. 0 through 4  
e. Any of `score[0]`, `score[1]`, `score[2]`, `score[3]`, `score[4]`

**3.** a. One too many initializers  
b. Correct. The array size is 4.  
c. Correct. The array size is 4.

**4.** `abc`

**5.**

```
1.1 2.2 3.3
1.1 3.3 3.3
```

(Remember that the indexes start with 0, not 1.)

**6.** `2 4 6 8 10 12 14 16 18 0 4 8 12 16`

**7.** The indexed variables of `sampleArray` are `sampleArray[0]` through `sampleArray[9]`, but this piece of code tries to fill `sampleArray[1]` through `sampleArray[10]`. The index 10 in `sampleArray[10]` is out of range.

**8.** There is an index out of range. When index is equal to 9, `index + 1` is equal to 10, so `a[index + 1]`, which is the same as `a[10]`, has an illegal index. The loop should stop with one less iteration. To correct the code, change the first line of the `for` loop to

```cpp
for (int index = 0; index < 9; index++)
```

**9.**

```cpp
int i, a[20];

cout << "Enter 20 numbers:\n";

for (i = 0; i < 20; i++)
    cin >> a[i];
```

**10.** The array will consume 14 bytes of memory. The address of the indexed variable `yourArray[3]` is 1006.

**11.** The following function calls are acceptable:

```cpp
tripler(number);
tripler(a[2]);
tripler(a[number]);
```

The following function calls are incorrect:

```cpp
tripler(a[3]);
tripler(a);
```

The first one has an illegal index. The second has no indexed expression at all. You cannot use an entire array as an argument to `tripler`, as in the second call. The section “Entire Arrays as Function Arguments” discusses a different situation in which you can use an entire array as an argument.

**12.** The loop steps through indexed variables `b[1]` through `b[5]`, but 5 is an illegal index for the array `b`. The indexes are 0, 1, 2, 3, and 4. The correct version of the code is:

```cpp
int b[5] = {1, 2, 3, 4, 5};
for (int i = 0; i < 5; i++)
    tripler(b[i]);
```

**13.**

```cpp
void oneMore(int a[], int size)
//Precondition: size is the declared size of the array a.
//a[0] through a[size − 1] have been given values.
//Postcondition: a[index] has been increased by 1
//for all indexed variables of a.
{
    for (int index = 0; index < size; index++)
        a[index] = a[index] + 1;
}
```

**14.** The following function calls are all acceptable:

```cpp
too2(myArray, 29);
too2(myArray, 10);
too2(yourArray, 100);
```

The call

```cpp
too2(myArray, 10);
```

is legal, but will fill only the first ten indexed variables of `myArray`. If that is what is desired, the call is acceptable.

The following function calls are all incorrect:

```cpp
too2(myArray, 55);
"Hey too2. Please, come over here."
too2(myArray[3], 29);
```

The first of these is incorrect because the second argument is too large. The second is incorrect because it is missing a final semicolon (and for other reasons). The third one is incorrect because it uses an indexed variable for an argument where it should use the entire array.

**15.** You can make the array parameter in `output` a constant parameter, since there is no need to change the values of any indexed variables of the array parameter. You cannot make the parameter in `dropOdd` a constant parameter because it may have the values of some of its indexed variables changed.

```cpp
void output(const double a[], int size);
//Precondition: a[0] through a[size - 1] have values.
//Postcondition: a[0] through a[size - 1] have been
//written out.
```

```cpp
void dropOdd(int a[], int size);
//Precondition: a[0] through a[size - 1] have values.
//Postcondition: All odd numbers in a[0] through
//a[size - 1] have been changed to 0.
```

**16.**

```cpp
int outOfOrder(double array[], int size)
{
    for (int i = 0; i < size - 1; i++)
        if (array[i] > array[i+1]) //fetch a[i+1] for each i.
            return i+1;
    return -1;
}
```

**17.**

```cpp
#include <iostream>
using namespace std;
const int DECLARED_SIZE = 10;

int main()
{
    cout << "Enter up to ten nonnegative integers.\n"
         << "Place a negative number at the end.\n";
    int numberArray[DECLARED_SIZE], next, index = 0;
    cin >> next;
    while ( (next >= 0) && (index < DECLARED_SIZE) )
    {
        numberArray[index] = next;
        index++;
        cin >> next;
    }
    int numberUsed = index;
    cout << "Here they are back at you:";
    for (index = 0; index < numberUsed; index++)
        cout << numberArray[index] << " ";
    cout << endl;
    return 0;
}
```

**18.**

```cpp
#include <iostream>
using namespace std;
const int DECLARED_SIZE = 10;

int main()
{
    cout << "Enter up to ten letters"
         << " followed by a period:\n";
    char letterBox[DECLARED_SIZE], next;
    int index = 0;
    cin >> next;
    while ( (next != '.') && (index < DECLARED_SIZE) )
    {
        letterBox[index] = next;
        index++;
        cin >> next;
    }
    int numberUsed = index;
    cout << "Here they are backwards:\n";
    for (index = numberUsed - 1; index >= 0; index--)
        cout << letterBox[index];
    cout << endl;
    return 0;
}
```

**19.**

```cpp
bool search(const int a[], int numberUsed, int target, int& where)
{
    int index = 0;
    bool found = false;
    while ((!found) && (index < numberUsed))
        if (target == a[index])
            found = true;
        else
            index++;
    //If target was found, then
    //found == true and a[index] == target.
    if (found)
        where = index;
    return found;
}
```

**20.**

```
0 1 2 3
0 1 2 3
0 1 2 3
0 1 2 3
```

**21.**

```cpp
int a[4][5];
int index1, index2;
for (index1 = 0; index1 < 4; index1++)
    for (index2 = 0; index2 < 5; index2++)
        cin >> a[index1][index2];
```

**22.**

```cpp
void echo(const int a[][5], int sizeOfA)
//Outputs the values in the array a on sizeOfA lines
//with 5 numbers per line.
{
    for (int index1 = 0; index1 < sizeOfA; index1++)
    {
        for (int index2 = 0; index2 < 5; index2++)
            cout << a[index1][index2] << " ";
        cout << endl;
    }
}
```

## Practice Programs

Practice Programs can generally be solved with a short program that directly applies the programming principles presented in this chapter.

**1.** Write a function called `findMax` which takes as input an array of `double`s which are greater than zero and an integer which specifies how many elements there are in the array. The function should return the largest value in the array. Write a driver program to test your function with arrays of different lengths, different values, and finally, test your function on an uninitialized array.

**2.** Write a function called `sumAll` which takes as input an array of integer values and an integer which specifies how many elements there are in the array. The function should return the sum of all the elements in the array. Write a driver program to test your function with arrays of different lengths, different values, and finally, test your function on an uninitialized array.

**3.** Write a void function called `normalizeArray` that takes as input an array of integers, an empty array of type `double`, and an integer which specifies the size of the arrays. Your function should copy the integer array and create a normalized version of it in the array of doubles. To do this, copy each element from the original array to the second array after dividing it by the sum of the elements of the original array. Use the `sumAll` function created in Practice Problem 2 to calculate the sum of all elements in the integer array.

**4.** The following code creates a small phone book. An array is used to store a list of names and another array is used to store the phone numbers that go with each name. For example, Michael Myers’ phone number is 333-8000 and Ash Williams’ phone number is 333-2323. Write the function `lookupName` so the code properly looks up and returns the phone number for the input target name.

```cpp
int main()
{
    using namespace std;
    string names[] = {"Michael Myers",
                      "Ash Williams",
                      "Jack Torrance",
                      "Freddy Krueger"};
    string phoneNumbers[] = {"333-8000","333-2323",
                             "333-6150","339-7970"};
    string targetName, targetPhone;
    char c;
    do
    {
        cout << "Enter a name to find the "
             << "corresponding phone number."
             << endl;
        getline(cin, targetName);
        targetPhone = lookupName(targetName,
                                 names, phoneNumbers, 4);
        if (targetPhone.length() > 0)
            cout << "The number is: "
                 << targetPhone << endl;
        else
            cout << "Name not found. "
                 << endl;
        cout << "Look up another name? (y/n)"
             << endl;
```
