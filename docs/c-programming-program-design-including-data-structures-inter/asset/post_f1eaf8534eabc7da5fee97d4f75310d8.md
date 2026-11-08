
Figure 8–11 shows the elements of `list` during the second iteration.

![](img/dc1b115c1ae2ec0d8a557b7c2b830e8c_575_0.png)

**FIGURE 8–11** Elements of list during the second iteration

Now the unsorted list is `list[1]...list[7]`. So, we find the smallest element in the unsorted list. The smallest element is at position 3, as shown in Figure 8–11(a). Because the smallest element in the unsorted list is at position 3, it must be moved to position 1. So, we swap 7 (that is, `list[3]`) with 30 (that is, `list[1]`), as shown in Figure 8–11(b). After swapping `list[1]` with `list[3]`, the resulting list is as shown in Figure 8–11(c).

Now, the unsorted list is `list[2]...list[7]`. So, we repeat the preceding process of finding the position of the smallest element in the unsorted portion of the list and moving it to the beginning of the unsorted portion of the list. Selection sort thus involves the following steps.

In the unsorted portion of the list:

- a. Find the location of the smallest element.
- b. Move the smallest element to the beginning of the unsorted list.

Initially, the entire list (that is, `list[0]...list[length - 1]`) is the unsorted list. After executing Steps a and b once, the unsorted list is `list[1]...list[length - 1]`. After executing Steps a and b a second time, the unsorted list is `list[2]...list[length - 1]`, and so on. This way, we can keep track of the unsorted portion of the list and repeat Steps a and b with the help of a `for` loop, as shown in the following pseudocode:

```text
for (index = 0; index < length - 1; index++)
{
    a.  Find the location, smallestIndex, of the smallest element in
        list[index]...list[length - 1].
    b.  Swap the smallest element with list[index]. That is, swap
        list[smallestIndex] with list[index].
}
```

The first time through the loop, we locate the smallest element in `list[0]...list[length - 1]` and swap the smallest element with `list[0]`. The second time through the loop, we locate the smallest element in `list[1]...list[length - 1]` and swap the smallest element with `list[1]`, and so on.

Step a is similar to the algorithm for finding the index of the largest item in the list, as discussed earlier in this chapter. (Also see Programming Exercise 2 at the end of this chapter.) Here, we find the index of the smallest item in the list. The general form of Step a is:

```cpp
    smallestIndex = index;  //assume first element is the smallest

    for (location = index + 1; location < length; location++)
        if (list[location] < list[smallestIndex])
            smallestIndex = location;  //current element in the list
                                       //is smaller than the smallest so
                                       //far, so update smallestIndex
```

Step b swaps the contents of `list[smallestIndex]` with `list[index]`. The following statements accomplish this task:

```cpp
    temp = list[smallestIndex];
    list[smallestIndex] = list[index];
    list[index] = temp;
```

It follows that to swap the values, three item assignments are needed. The following function, `selectionSort`, implements the selection sort algorithm:

```cpp
    void selectionSort(int list[], int length)
    {
        int index;
        int smallestIndex;
        int location;
        int temp;

        for (index = 0; index < length - 1; index++)
        {
            //Step a
            smallestIndex = index;

            for (location = index + 1; location < length; location++)
                if (list[location] < list[smallestIndex])
                    smallestIndex = location;

            //Step b
            temp = list[smallestIndex];
            list[smallestIndex] = list[index];
            list[index] = temp;
        }
    }
```

The program in Example 8-9 illustrates how to use the selection sort algorithm in a program.

### EXAMPLE 8-9

```cpp
//Selection sort

#include <iostream>

using namespace std;

void selectionSort(int list[], int length);

int main()
{
    int list[] = {2, 56, 34, 25, 73, 46, 89, 10, 5, 16};    //Line 1
    int i;                                                   //Line 2

    selectionSort(list, 10);                                //Line 3

    cout << "After sorting, the list elements are:" << endl; //Line 4
    for (i = 0; i < 10; i++)                                //Line 5
        cout << list[i] << " ";                             //Line 6

    cout << endl;                                            //Line 7

    return 0;                                                //Line 8
}

//Place the definition of the function selectionSort given
//previously here.
```

### Sample Run:

```text
After sorting, the list elements are:
2 5 10 16 25 34 46 56 73 89
```

The statement in Line 1 declares and initializes `list` to be an array of 10 components of type `int`. The statement in Line 3 uses the function `selectionSort` to sort `list`. Notice that both `list` and its length (the number of elements in it, which is 10) are passed as parameters to the function `selectionSort`. The `for` loop in Lines 5 and 6 outputs the elements of `list`.

To illustrate the selection sort algorithm in this program, we declared and initialized the array `list`. However, you can also prompt the user to input the data during program execution.

For a list of length *n*, selection sort makes exactly \(\frac{n(n-1)}{2}\) key comparisons and \(3(n-1)\) item assignments. Therefore, if *n* = 1000, then to sort the list, selection sort makes about 500,000 key comparisons and about 3000 item assignments. The next section presents the insertion sort algorithm that reduces the number of comparisons.

## C-Strings (Character Arrays)

Until now, we have avoided discussing character arrays for a simple reason: Character arrays are of special interest, and you process them differently than you process other arrays. C++ provides many (predefined) functions that you can use with character arrays.

**Character array:** An array whose components are of type `char`.

Recall that the most widely used character sets are ASCII and EBCDIC. The first character in the ASCII character set is the null character, which is nonprintable. Also, recall that in C++, the null character is represented as `'\0'`, a backslash followed by a zero.

The statement:

```cpp
ch = '\0';
```

stores the null character in `ch`, wherein `ch` is a `char` variable.

As you will see, the null character plays an important role in processing character arrays. Because the collating sequence of the null character is 0, the null character is less than any other character in the `char` data set.

The most commonly used term for character arrays is C-strings. However, there is a subtle difference between character arrays and C-strings. Recall that a string is a sequence of zero or more characters, and strings are enclosed in double quotation marks. In C++, C-strings are null terminated; that is, the last character in a C-string is always the null character. A character array might not contain the null character, but the last character in a C-string is always the null character. As you will see, the null character should not appear anywhere in the C-string except at the last position. Also, C-strings are stored in (one-dimensional) character arrays.

The following are examples of C-strings:

```text
"John L. Johnson"
"Hello there."
```

From the definition of C-strings, it is clear that there is a difference between `'A'` and `"A"`. The first one is character A; the second is C-string A. Because C-strings are null terminated, `"A"` represents two characters: `'A'` and `'\0'`. Similarly, the C-string `"Hello"` represents six characters: `'H'`, `'e'`, `'l'`, `'l'`, `'o'`, and `'\0'`. To store `'A'`, we need only one memory cell of type `char`; to store `"A"`, we need two memory cells of type `char`—one for `'A'` and one for `'\0'`. Similarly, to store the C-string `"Hello"` in computer memory, we need six memory cells of type `char`.

Consider the following statement:

```cpp
char name[16];
```

This statement declares an array `name` of 16 components of type `char`. Because C-strings are null terminated and `name` has 16 components, the largest string that can be stored in `name` is of length 15. If you store a C-string of length 10 in `name`, the first 11 components of `name` are used and the last 5 are left unused.

The statement:

```cpp
char name[16] = {'J', 'o', 'h', 'n', '\0'};
```

declares an array `name` containing 16 components of type `char` and stores the C-string `"John"` in it. During `char` array variable declaration, C++ allows the C-string notation to be used in the initialization statement. The above statement is, therefore, equivalent to:

```cpp
char name[16] = "John";          //Line A
```

Recall that the size of an array can be omitted if the array is initialized during the declaration.

The statement:

```cpp
char name[] = "John";            //Line B
```

declares a C-string variable `name` of a length large enough—in this case, 5—and stores `"John"` in it. There is a difference between the last two statements: Both statements store `"John"` in `name`, but the size of `name` in the statement in Line A is 16, and the size of `name` in the statement in Line B is 5.

Most rules that apply to other arrays also apply to character arrays. Consider the following statement:

```cpp
char studentName[26];
```

Suppose you want to store `"Lisa L. Johnson"` in `studentName`. Because aggregate operations, such as assignment and comparison, are not allowed on arrays, the following statement is not legal:

```cpp
studentName = "Lisa L. Johnson"; //illegal
```

C++ provides a set of functions that can be used for C-string manipulation. The header file `cstring` describes these functions. We often use three of these functions: `strcpy` (string copy, to copy a C-string into a C-string variable—that is, assignment); `strcmp`
