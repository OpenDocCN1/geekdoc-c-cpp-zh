
- 22. It is very easy to replace the space with any character.

    ```cpp
    /**
      @param str any string
      @param ch a string of length 1
      @return the number of times that ch occurs in str
    */
    int count(string str, string ch)
    {
       int count = 0;
       for (int i = 0; i < str.length(); i++)
       {
          if (str.substr(i, 1) == ch) { count++; }
       }
       return count;
    }
    ```

    This is useful if you want to count other characters. For example, `count(input, ",")` counts how many commas are in the input.

- 23. Change line 75 to

    ```cpp
    name = name + digit_name(part / 100) + " hundred";
    ```

    In line 72, add the statement

    ```cpp
    if (part >= 1000)
    {
        name = digit_name(part / 1000) + "thousand ";
        part = part % 1000;
    }
    ```

    In line 65, change 1000 to 10000 in the comment.

- 24. In the case of "teens", we already have the last digit as part of the name.

- 25. Nothing is printed. One way of dealing with this case is to add the following statement before line 70.

    ```cpp
    if (number == 0) { return "zero"; }
    ```

- 26. Here is the approximate trace:

    | int name(number = 72) | |
    | --- | --- |
    | **part** | **name** |
    | <s>72</s> | <s>"seventy"</s> |
    | 2 | "seventy two" |

    Note that the string starts with a blank space. Exercise P5.18 asks you to eliminate it.

- 27. Here is one possible solution. Break up the task `print table` into `print header` and `print body`. The `print header` task calls `print separator`, prints the header cells, and calls `print separator` again. The `print body` task repeatedly calls `print row` and then calls `print separator`.

- 28. 1.

- 29. 2, 7.

- 30. Lines 3, 4, 5, 6, 10, 11, but not 7 through 9.

- 31. The global variable defined in line 1.

## Syntax 6.1 — Defining an Array

![](img/23fb3582e93ebc95909e1de029c3d388_278_0.png)

Here we define an array that can hold ten values:

```cpp
double values[10];
```

This is the definition of a variable values whose type is "array of double". That is, values stores a sequence of floating-point numbers. The [10] indicates the size of the array. (See Figure 1.) The array size must be a constant that is known at compile time.

When you define an array, you can specify the initial values. For example,

```cpp
double values[] = { 32, 54, 67.5, 29, 34.5, 80, 115, 44.5, 100, 65 };
```

When you supply initial values, you don't need to specify the array size. The compiler determines the size by counting the values.

> Use an array to collect a sequence of values of the same type.

**Table 1 — Defining Arrays**

| Declaration | Description |
| --- | --- |
| `int numbers[10];` | An array of ten integers. |
| `const int SIZE = 10;`<br>`int numbers[SIZE];` | It is a good idea to use a named constant for the size. |
| `int size = 10;`<br>`int numbers[size];` | **Caution:** In standard C++, the size must be a constant. This array definition will not work with all compilers. |
| `int squares[5] = { 0, 1, 4, 9, 16 };` | An array of five integers, with initial values. |
| `int squares[] = { 0, 1, 4, 9, 16 };` | You can omit the array size if you supply initial values. The size is set to the number of initial values. |
| `int squares[5] = { 0, 1, 4 };` | If you supply fewer initial values than the size, the remaining values are set to 0. This array contains 0, 1, 4, 0, 0. |
| `string names[3];` | An array of three strings. |

### 6.1.2 Accessing Array Elements

Individual elements in an array `values` are accessed by an integer index *i*, using the notation `values[i]`.

The values stored in an array are called its **elements**. Each element has a position number, called an **index**. To access a value in the values array, you must specify which index you want to use. That is done with the `[]` operator:

```cpp
values[4] = 34.5;
```

Now the element with index 4 is filled with 34.5. (See Figure 2).

![](img/23fb3582e93ebc95909e1de029c3d388_279_0.png)

**Figure 2**
Filling an Array Element

You can display the contents of the element with index 4 with the following command:

```cpp
cout << values[4] << endl;
```

As you can see, the element values[4] can be used like any variable of type double.

An array element can be used like any variable.

In C++, array positions are counted in a way that you may find surprising. If you look carefully at Figure 2, you will find that the *fifth* element was filled when we changed values[4]. In C++, the elements of arrays are numbered *starting at 0*. That is, the legal elements for the values array are

- values[0], the first element
- values[1], the second element
- values[2], the third element
- values[3], the fourth element
- values[4], the fifth element
- ...
- values[9], the tenth element

An array index must be at least zero and less than the size of the array.

You will see in Chapter 7 why this numbering scheme was chosen in C++.

You have to be careful about index values. Trying to access an element that does not exist in the array is a serious error. For example, if values has twenty elements, you are not allowed to access values[20].

Attempting to access an element whose index is not within the valid index range is called a **bounds error**. The compiler does not catch this type of error. Even the running program generates *no* error message. If you make a bounds error, you silently read or overwrite another memory location. As a consequence, your program may have random errors, and it can even crash.

*Like a post office box that is identified by a box number, an array element is identified by an index.*

![](img/23fb3582e93ebc95909e1de029c3d388_279_1.png)

A bounds error, which occurs if you supply an invalid array index, can corrupt data or cause your program to terminate.

The most common bounds error is the following:

```cpp
double values[10];
cout << values[10];
```

There is no `values[10]` in an array with ten elements—the legal index values range from 0 to 9.

To visit all elements of an array, use a variable for the index. Suppose `values` has ten elements and the integer variable `i` takes values 0, 1, 2, and so on, up to 9. Then the expression `values[i]` yields each element in turn. For example, this loop displays all elements.

```cpp
for (int i = 0; i < 10; i++)
{
    cout << values[i] << endl;
}
```

Note that in the loop condition the index is *less than* 10 because there is no element corresponding to `values[10]`.

### 6.1.3 Partially Filled Arrays

![](img/23fb3582e93ebc95909e1de029c3d388_280_0.png)

*With a partially filled array, you need to remember how many elements are filled.*

An array cannot change size at run time. This is a problem when you don't know in advance how many elements you need. In that situation, you must come up with a good guess on the maximum number of elements that you need to store. We call this quantity the *capacity*. For example, we may decide that we sometimes want to store more than ten values, but never more than 100:

```cpp
const int CAPACITY = 100;
double values[CAPACITY];
```

In a typical program run, only part of the array will be occupied by actual elements. We call such an array a *partially filled array*. You must keep a companion variable that counts how many elements are actually used. In Figure 3 we call the companion variable `current_size`.

![](img/23fb3582e93ebc95909e1de029c3d388_280_1.png)

**Figure 3**
*A Partially Filled Array*

With a partially filled array, keep a companion variable for the current size.

The following loop collects values and fills up the `values` array.

```cpp
int current_size = 0;
double input;
while (cin >> input)
{
    if (current_size < CAPACITY)
    {
        values[current_size] = input;
        current_size++;
    }
}
```
