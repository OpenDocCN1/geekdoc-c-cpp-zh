
typedef double LittleDouble[LITTLE];
LittleDouble value;

Tell what value (if any) will be assigned to each array element, or explain why an error occurs:

```
1. for (i = 0; i < MEDIUM; i++)
    number[i] = i / 2;
```

```
2. for (i = 0; i < LITTLE; i++)
    number[i] = i * i;
for (i = LITTLE; i < MEDIUM; i++)
    number[i] = number[i - 5];
```

```
3. for (i = 0; i < 3; i++)
    value[i] = 0;
for (i = 3; i < LITTLE; i++)
    value[i] = 1;
```

```
4. for (i = 1; i < LITTLE; i += 2)
{
    value[i - 1] = double(i) / 2.0;
    value[i] = 10.0 * value[i - 1];
}
```

```
5. i = 0;
while (i != 10)
{
    if (i % 3 == 0)
        number[i] = 0;
    else
        number[i] = i;
    i++;
}
```

```
6. number[1] = 1;
i = 2;
do
{
    number[i] = 2 * number[i - 1];
    i++;
}
while (i < MEDIUM);
```

```
7. for (ch = 'A'; ch <= 'F'; ch++)
    if (ch == 'A')
        letterCount[ch] = 1;
    else
        letterCount[ch] = letterCount[ch - 1] + 1;
```

```
8. for (i = 0; i < n - 1; i++)
    for (j = 0; j < n - i - 1; j++)
        if (number[j] > number[j + 1])
        {
            temp = number[j];
            number[j] = number[j + 1];
            number[j + 1] = temp;
        }
```

For Exercises 9–14, write definitions of the given arrays in two ways: (a) without using typedef and (b) using typedef.

+   9. An array with capacity 10 in which each element is an integer.
+   10. An array whose indices are integers from 0 through 10 and in which each element is a real value.
+   11. An array with capacity 10 in which each element is an integer, all of which are initially 0.
+   12. An array that can store five strings.
+   13. An array that can store five characters and is initialized with the vowels a, e, i, o, and u.
+   14. An array that can store 100 values, each of which is either true or false.

For Exercises 15–18, write definitions and statements to construct the given array.

+   15. An array whose indices are the integers from 0 through 99 and in which the value stored in each element is the same as the index.
+   16. An array whose indices are the integers from 0 through 99 and in which the values stored in the elements are the indices in reverse order.
+   17. An array of capacity 50 in which the value stored in an element is true if the corresponding index is even and false otherwise.
+   18. An array whose indices are the decimal ASCII values (0-127), such that the value stored in an element is true if the index is that of a vowel, and false otherwise.

19. Return the smallest value stored in an array of integers.

20. Return the largest value stored in an array of integers.

21. Return the range of values stored in an array of integers, that is, the difference between the largest value and the smallest value.

22. Return true if the values stored in an array are in ascending order and false otherwise.

23. Insert a value into an array of integers at a specified position in the array.

24. Remove a value from an array of integers at a specified position in the array.

## Section 12.3

For each of the arrays x in Exercises 1–4, show x after each of the first four passes of simple selection sort.

| i | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 |
|---|---|---|---|---|---|---|---|---|
| x[i] | 30 | 50 | 80 | 10 | 60 | 20 | 70 | 40 |

| i | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 |
|---|---|---|---|---|---|---|---|---|
| x[i] | 20 | 40 | 70 | 60 | 80 | 50 | 30 | 10 |

| i | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 |
|---|---|---|---|---|---|---|---|---|
| x[i] | 80 | 70 | 60 | 50 | 40 | 30 | 20 | 10 |

| i | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 |
|---|---|---|---|---|---|---|---|---|
| x[i] | 10 | 20 | 30 | 40 | 50 | 60 | 70 | 80 |

5. One variation of simple selection sort for a list stored in an array x[0],..., x[n-1] is to locate both the smallest and the largest elements while scanning the list and to position them at the beginning and the end of the list, respectively. On the next scan, this process is repeated for the sublist x[1],..., x[n-2], and so on. Write an algorithm to implement this double-ended selection sort.

6.–9. For the arrays x in Exercises 1–4 show x after each pass of the double-ended selection sort described in Exercise 5.

## Section 12.6

For Exercises 1–10, assume that the following declarations have been made,

```
vector<int> number,
    v(10,20),
    w(10);
int num;
```

and that for exercises that involve input, the following values are entered:

```
99 33 44 88 22 11 55 66 77 -1
```

Describe the contents of the given vector<T> after the statements are executed.

```
1. for (int i = 0; i < 10; i++)
    number.push_back(i / 2);
```

```
2. for (int i = 0; i < 6; i++)
    w.push_back(i / 2);
```

```
3. for (;;)
{
    cin >> num;
    if (num < 0) break;
    number.push_back(num);
}
```

```
4. for (int i = 0; i <= 5; i++)
    number.push_back(i);
for (int i = 0; i < 2; i++)
    number.pop_back();
for (int i = 0; i <= 5; i++)
    number.push_back(i);
```

For Exercises 5–10 assume that the loop in Exercise 3 has been executed.

```
5. for (int i = 0; i < number.size() - 1; i += 2)
    number[i] = number[i + 1];
```

```
6. number.pop_back();
    number.push_back(number.front());
```

```
7. int temp = number.front();
    number.front() = number.back();
    number.back() = temp;
```

```
8. sort(number.begin(), number.end());
```

```
9. for (int i = 0; i < number.size(); i++)
    w.push_back(number[i] + v[i]);
```

```
10. while (v < number)
{
    v.erase(v.begin());
    number.erase(number.begin());
}
```

For Exercises 11–15 write a declaration for a vector<T> having the given properties.

+   11. Can store long int values.
+   12. Capacity 10 and each element is a long int.
+   13. Capacity 10 and each element is a long int, all of which are initially 0.
+   14. Capacity 5, size 5, and each element contains a string, initially "xxx".
+   15. Capacity 100 and each element is either true or false.

For Exercises 16–18, write definitions and statements to construct a vector<T> with the required properties.

+   16. Stores the sequence of integers from 0 through 99.
+   17. Stores the sequence of integers from 0 through 99 in reverse order.
+   18. Has capacity 50, and the value stored in an element is true if the corresponding index is even and is false otherwise.

Exercises 19–25 ask you to write functions to do various things. To test these functions, you should write driver programs as instructed in Programming Problems 1–3 of Section 12.6.

+   19. Returns true if the values stored in a vector<double> are in ascending order and false otherwise.
+   20. Finds the range of values stored in a vector<double>, that is, the difference between the largest value and the smallest value.

Exercises 21–25 deal with operations on n-dimensional vectors, which are sequences of n real numbers and which are studied and used in many areas of mathematics and science. They can obviously be modeled in C++ by vector<double>s of capacity n. In the description of each operation, A and B are assumed to be n-dimensional vectors:

A = (a₁, a₂, ..., aₙ)
B = (b₁, b₂, ..., bₙ)

21. Compute and return the sum of two n-dimensional vectors:

$A + B = (a_1 + b_1, a_2 + b_2, \dots, a_n + b_n)$

22. Compute and return the difference of two n-dimensional vectors:

$A - B = (a_1 - b_1, a_2 - b_2, \dots, a_n - b_n)$

23. Compute and return the product of a scalar (real number) and an n-dimensional vector:

$cA = (ca_1, ca_2, \dots, ca_n)$

24. Compute and return the magnitude of an n-dimensional vector:

$|A| = \sqrt{a_1^2 + a_2^2 + \dots + a_n^2}$

25. Compute and return the inner (or dot) product of two n-dimensional vectors (which is a scalar):

$A \cdot B = a_1 \times b_1 + a_2 \times b_2 + \dots + a_n \times b_n = \sum_{i=1}^n (a_i \times b_i)$

## PROGRAMMING PROBLEMS

+   1. Write a driver program to test the smallest-element function of Exercise 19.
+   2. Write a driver program to test the largest-element function of Exercise 20.
+   3. Write a driver program to test the range function of Exercise 21.
+   4. Write a driver program to test the ascending-order function of Exercise 22.
+   5. Write a driver program to test the insert function of Exercise 23.
+   6. Write a driver program to test the remove function of Exercise 24.
+   7. The Rinky Dooflingy Company records the number of cases of dooflinggies produced each day over a four-week period. Write a program that reads these production numbers and stores them in an array. The program should then accept from the user a week number and a day number, and should display the production level for that day. Assume that each week consists of five workdays.
+   8. The Rinky Dooflingy Company maintains two warehouses, one in Chicago and one in Detroit, each of which stocks at most 25 different items. Write a program that first
