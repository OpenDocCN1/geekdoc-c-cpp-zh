
## Display 5.9 Two-dimensional Array (part 3 of 3)

```cpp
{
    for (int quizNum = 1; quizNum <= NUMBER_QUIZZES; quizNum++)
    {//Process one quiz (for all students):
        double sum = 0;
        for (int stNum = 1; stNum <= NUMBER_STUDENTS; stNum++)
            sum = sum + grade[stNum-1][quizNum-1];
        //sum contains the sum of all student scores on quiz number quizNum.
        quizAve[quizNum-1] = sum/NUMBER_STUDENTS;
        //Average for quiz quizNum is the value of quizAve[quizNum-1]
    }
}

void display(const int grade[][NUMBER_QUIZZES],
             const double stAve[], const double quizAve[])
{
    cout.setf(ios::fixed);
    cout.setf(ios::showpoint);
    cout.precision(1);

    cout << setw(10) << "Student"
         << setw(5) << "Ave"
         << setw(15) << "Quizzes\n";
    for (int stNum = 1; stNum <= NUMBER_STUDENTS; stNum++)
    {//Display for one stNum:
        cout << setw(10) << stNum
             << setw(5) << stAve[stNum-1] << " ";
        for (int quizNum = 1; quizNum <= NUMBER_QUIZZES; quizNum++)
            cout << setw(5) << grade[stNum-1][quizNum-1];
        cout << endl;
    }

    cout << "Quiz averages = ";
    for (int quizNum = 1; quizNum <= NUMBER_QUIZZES; quizNum++)
        cout << setw(5) << quizAve[quizNum-1];
    cout << endl;
}
```

## SAMPLE DIALOGUE

> _<The dialogue for filling the array grade is not shown.>_

| Student | Ave | Quizzes |
|---:|---:|:---|
| 1 | 10.0 | 10  10  10 |
| 2 | 1.0 | 2  0  1 |
| 3 | 7.7 | 8  6  9 |
| 4 | 7.3 | 8  4  10 |
| **Quiz Average** |  | **7.0  5.0  7.5** |

## Display 5.10 The Two-Dimensional Array grade

![](img/9505fd46e120aa9c1406715936ff6251_208_0.png)

## Display 5.11 The Two-Dimensional Array grade

![](img/9505fd46e120aa9c1406715936ff6251_208_1.png)

## Self-Test Exercises

20. What is the output produced by the following code?

```
int myArray[4][4], index1, index2;
for (index1 = 0; index1 < 4; index1++)
    for (index2 = 0; index2 < 4; index2++)
        myArray[index1][index2] = index2;
for (index1 = 0; index1 < 4; index1++)
{
    for (index2 = 0; index2 < 4; index2++)
        cout << myArray[index1][index2] << " ";
    cout << endl;
}
```

21. Write code that will fill the array a (declared below) with numbers typed in at the keyboard. The numbers will be input five per line, on four lines (although your solution need not depend on how the input numbers are divided into lines).

```
int a[4][5];
```

22. Write a function definition for a void function called echo such that the following function call will echo the input described in Self-Test Exercise 21, and will echo it in the same format as we specified for the input (that is, four lines of five numbers per line):

```
echo(a, 4);
```

## Chapter Summary

- An array can be used to store and manipulate a collection of data that is all of the same type.
- The indexed variables of an array can be used just like any other variables of the base type of the array.
- A for loop is a good way to step through the elements of an array and perform some program action on each indexed variable.
- The most common programming error made when using arrays is attempting to access a nonexistent array index. Always check the first and last iterations of a loop that manipulates an array to make sure it does not use an index that is illegally small or illegally large.
- An array formal parameter is neither a call-by-value parameter nor a call-by-reference parameter, but a new kind of parameter. An array parameter is similar to a call-by-reference parameter in that any change that is made to the formal parameter in the body of the function will be made to the array argument when the function is called.
- The indexed variables for an array are stored next to each other in the computer’s memory so that the array occupies a contiguous portion of memory. When the array is passed as an argument to a function, only the address of the first indexed variable (the one numbered 0) is given to the calling function. Therefore, a function with an array parameter usually needs another formal parameter of type int to give the size of the array.
- When using a partially filled array, your program needs an additional variable of type int to keep track of how much of the array is being used.
- To tell the compiler that an array argument should not be changed by your function, you can insert the modifier const before the array parameter for that argument position. An array parameter that is modified with a const is called a constant array parameter.
- If you need an array with more than one index, you can use a multidimensional array, which is actually an array of arrays.

## ANSWERS TO SELF-TEST EXERCISES

- 1. The statement `int a[5];` is a declaration, in which 5 is the number of array elements. The expression `a[4]` is an access into the array defined by the previous statement. The access is to the element having index 4, which is the fifth (and last) array element.
- 2. a. `score`
  b. `double`
  c. `5`
  d. `0 through 4`
  e. Any of `score[0]`, `score[1]`, `score[2]`, `score[3]`, `score[4]`
- 3. a. One too many initializers
  b. Correct. The array size is 4.
  c. Correct. The array size is 4.
- 4. `abc`
- 5.
  ```text
  1.1 2.2 3.3
  1.1 3.3 3.3
  ```
  (Remember that the indexes start with 0, not 1.)
- 6.
  ```text
  0  2  4  6  8  10  12  14  16  18
  0  4  8  12  16
  ```
- 7. The indexed variables of `sampleArray` are `sampleArray[0]` through `sampleArray[9]`, but this piece of code tries to fill `sampleArray[1]` through `sampleArray[10]`. The index 10 in `sampleArray[10]` is out of range.
- 8. There is an index out of range. When index is equal to 9, index + 1 is equal to 10, so a[index + 1], which is the same as a[10], has an illegal index. The loop should stop with one fewer iteration. To correct the code, change the first line of the for loop to

```
for (int index = 0; index < 9; index++)
```
- 9. int i, a[20];
cout << "Enter 20 numbers:\n";
for (i = 0; i < 20; i++)
    cin >> a[i];
- 10. The array will consume 14 bytes of memory. The address of the indexed variable yourArray[3] is 1006.
- 11. The following function calls are acceptable:

```
tripler(a[2]);
tripler(a[number]);
tripler(number);
```

The following function calls are incorrect:

```
tripler(a[3]);
tripler(a);
```

The first one has an illegal index. The second has no indexed expression at all. You cannot use an entire array as an argument to tripler, as in the second call. The section Entire Arrays as Function Arguments discusses a different situation in which you can use an entire array as an argument.
- 12. The loop steps through indexed variables b[1] through b[5], but 5 is an illegal index for the array b. The indexes are 0, 1, 2, 3, and 4. The correct version of the code is given below:

```
int b[5] = {1, 2, 3, 4, 5};
for (int i = 0; i < 5; i++)
    tripler(b[i]);
```
- 13. void oneMore(int a[], int size)
//Precondition: size is the declared size of the array a.
//a[0] through a[size-1] have been given values.
//Postcondition: a[index] has been increased by 1
//for all indexed variables of a.
{
    for (int index = 0; index < size; index++)
        a[index] = a[index] + 1;
}
- 14. The following function calls are all acceptable:

too2(myArray, 29);  
too2(myArray, 10);  
too2(yourArray, 100);

The call

too2(myArray, 10);

is legal, but will fill only the first ten indexed variables of myArray. If that is what is desired, the call is acceptable.

The following function calls are all incorrect:

too2(myArray, 55);
“Hey too2. Please come over here.”
too2(myArray[3], 29);

The first of these is incorrect because the second argument is too large, the second because it is missing a final semicolon (and for other reasons), and the third because it uses an indexed variable for an argument where it should use the entire array.
- 15. You can make the array parameter in output a constant parameter, since there is no need to change the values of any indexed variables of the array parameter. You cannot make the parameter in dropOdd a constant parameter because it may have the values of some of its indexed variables changed.

```
void output(const double a[], int size)
//Precondition: a[0] through a[size − 1] have values.
//Postcondition: a[0] through a[size − 1] have been written out.

void dropOdd(int a[], int size);
//Precondition: a[0] through a[size − 1] have values.
//Postcondition: All odd numbers in a[0] through a[size − 1]
//have been changed to 0.
```
- 16. int outOfOrder(double array[], int size)
      {
          for(int i = 0; i < size − 1; i++)
              if (array[i] > array[i+1])//fetch a[i+1] for each i.
                  return i+1;
          return −1;
      }
- 17. #include <iostream>
    using namespace std;
    const int DECLARED_SIZE = 10;
    
    int main()
    {
        cout << "Enter up to ten nonnegative integers.\n"
