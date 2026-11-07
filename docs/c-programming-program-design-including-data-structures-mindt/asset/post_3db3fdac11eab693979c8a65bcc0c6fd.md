
| Function Name and Parameters | Parameter(s) Type | Function Return Value |
|---|---|---|
| `sqrt(x)` | x is a floating-point expression, in which x ≥ 0.0. | Square root of x |
| `tan(x)` | x is a floating-point expression; x is measured in radians | Trigonometric tangent of the angle |
| `tanh(x)` | x is a floating-point expression | Hyperbolic tangent of x |

## Header File `cstddef` (`stddef.h`)

Among others, this header file contains the definition of the following symbolic constant: **NULL**: the system-dependent null pointer (usually 0).

## Header File `cstring` (`string.h`)

The following table shows various string functions.

| Function Name and Parameters | Parameter(s) Type | Function Return Value |
|---|---|---|
| `strcat(destStr, srcStr)` | `destStr` and `srcStr` are null-terminated `char` arrays; `destStr` must be large enough to hold the result | The base address of `destStr` is returned; `srcStr`, including the null character, is concatenated to the end of `destStr`. |
| `strncat(destStr, srcStr, limit)` | `destStr` and `srcStr` are null-terminated `char` arrays; `destStr` must be large enough to hold the result; `limit` is a nonnegative integer value | This is the same as the previous function `strcat`, except that at most `limit` characters are appended. |
| `strcmp(str1, str2)` | `str1` and `str2` are null-terminated `char` arrays | The returned value is as follows:<br>• An `int` value < 0 if `str1 < str2`<br>• An `int` value 0 if `str1 == str2`<br>• An `int` value > 0 if `str1 > str2` |
| `strncmp(str1, str2, limit)` | `str1` and `str2` are null-terminated `char` arrays and `limit` is a nonnegative integer value | This is the same as the previous function `strcmp`, except that at most `limit` characters are compared. |
| `strcpy(destStr, srcStr)` | `destStr` and `srcStr` are null-terminated `char` arrays | The base address of `destStr` is returned; `srcStr` is copied into `destStr`. |
| `strncpy(destStr, srcStr, limit)` | `destStr` and `srcStr` are null-terminated `char` arrays and `limit` is a nonnegative integer value | Copies the string `srcStr` into the string variable `destStr`. At most `limit` characters are copied into `destStr`. |
| `strlen(str)` | `str` is a null-terminated `char` array | An integer value ≥ 0 specifying the length of the `str` (excluding the `\0`) is returned. |

## HEADER FILE `string`

This header file—not to be confused with the header file `cstring`—supplies a programmer-defined data type named `string`. Associated with the `string` type are a data type `string::size_type` and a named constant `string::npos`. These are defined as follows:

|  |  |
|---|---|
| `string::size_type` | An unsigned integer type |
| `string::npos` | The maximum value of type `string::size_type` |

The type string contains several functions for string manipulation. In addition to the string functions listed in Table 7-1, the following table describes additional string functions. In this table, we assume that `strVar` is a string variable and `str` is a string variable, a string constant, or a character array. The name of the function is shown in bold.

| Expression | Effect |
|---|---|
| `getline(istreamVar, strVar);` | `istreamVar` is an input stream variable (of type `istream` or `ifstream`).<br><br>Characters until the newline character are input from `istreamVar` and stored in `strVar`. (The newline character is read but not stored into `strVar`.) The value returned by this function is usually ignored. |
| `strVar.append(str, n);` | The first n characters of the character array `str` are appended to `strVar`. |
| `strVar.c_str()` | Returns the base address of a null-terminated C-string corresponding to the characters in `strVar`. |
| `strVar.capacity()` | Returns the size of the storage allocated for `strVar`. |
| `strVar.erase(pos);` | `pos` is a parameter of type `string::size_type`. Removes all of the characters from `strVar` starting at index `pos`. |
| `strVar.resize(n, ch);` | Changes the size of storage allocation for `strVar` to n. If n is less than the current storage size of `strVar`, the storage size of the string is truncated to n. If n is greater than the current storage size, the string is expanded to size n and the additional space is filled with copies of the character specified by `ch`. |

## APPENDIX G

### Memory Size on a System

A program similar to the following prints the memory size of the built-in data types on your system. (The output of the program shows the size of the built-in data type on which this program was run.)

```cpp
#include <iostream>

using namespace std;

int main()
{
    cout << "Size of char = " << sizeof(char) << endl;
    cout << "Size of int = " << sizeof(int) << endl;
    cout << "Size of short = " << sizeof(short) << endl;
    cout << "Size of unsigned int = " << sizeof(unsigned int)
         << endl;
    cout << "Size of long = " << sizeof(long) << endl;
    cout << "Size of long long = " << sizeof(long long)
         << endl;
    cout << "Size of bool = " << sizeof(bool) << endl;
    cout << "Size of float = " << sizeof(float) << endl;
    cout << "Size of double = " << sizeof(double) << endl;
    cout << "Size of long double = " << sizeof(long double)
         << endl;
    cout << "Size of unsigned short = "
         << sizeof(unsigned short) << endl;
    cout << "Size of unsigned long = "
         << sizeof(unsigned long) << endl;

    return 0;
}
```

Sample Run:

```
Size of char = 1
Size of int = 4
Size of short = 2
Size of unsigned int = 4
Size of long = 4
Size of long long = 8
Size of bool = 1
Size of float = 4
Size of double = 8
Size of long double = 8
Size of unsigned short = 2
Size of unsigned long = 4
```

![](img/b217c421655b51e7494cf3b89bb5432d_1668_0.png)

## APPENDIX H

### REFERENCES

© HunThomas/Shutterstock.com

- 1. G. Booch, *Object-Oriented Analysis and Design*, 2nd ed., Addison-Wesley, Reading, MA, 1995.
- 2. E. Horowitz, S. Sahni, and S. Rajasekaran, *Computer Algorithms C++*, Computer Science Press, 1997.
- 3. N.M. Josuttis, *The C++ Standard Library: A Tutorial and Reference*, Addison-Wesley, Reading, MA, 1999.
- 4. D.E. Knuth, *The Art of Computer Programming, Volume 1: Fundamental Algorithms*, 3rd ed., Addison-Wesley, Reading, MA, 1997.
- 5. D.E. Knuth, *The Art of Computer Programming, Volume 2: Seminumerical Algorithms*, 3rd ed., Addison-Wesley, Reading, MA, 1998.
- 6. D.E. Knuth, *The Art of Computer Programming, Volume 3: Searching and Sorting*, 2nd ed., Addison-Wesley, Reading, MA, 1998.
- 7. S.B. Lippman and J. Lajoie, *C++ Primer*, 3rd ed., Addison-Wesley, Reading, MA, 1998.
- 8. D.S. Malik and M.K. Sen, *Discrete Mathematics: Theory and Applications (Revised Edition)*, Cengage Learning Asia, Singapore, 2010.
- 9. E.M. Reingold and W.J. Hensen, *Data Structures in Pascal*, Little Brown and Company, Boston, MA, 1986.
- 10. R. Sedgewick, *Algorithms in C*, 3rd ed., Addison-Wesley, Reading, MA, Parts 1–4, 1998; Part 5, 2002.
- 11. B. Stroustrup, *The Design and Evolution of C++*, Addison-Wesley, Reading, MA, 1994.

![](img/b217c421655b51e7494cf3b89bb5432d_1670_0.png)

## APPENDIX I

### Answers to Odd-Numbered Exercises

### Chapter 1

- 1. a. true; b. false; c. false; d. true; e. false; f. true; g. true; h. true; i. false; j. false; k. true; l. true; m. true; n. true; o. true; p. false; q. true; r. true; s. true
- 3. Base 2 or binary.
- 5. In linking, an object program is combined with other programs in the library, used in the program, to create the executable code.
- 7. #
- 9. Programming is a process of problem solving.
- 11. (1) Analyze and outline the problem and its solution requirements, and design an algorithm to solve the problem. (2) Implement the algorithm in a programming language, such as C++, and verify that the algorithm works. (3) Maintain the program by using and modifying it if the problem domain changes.
- 13. To find the weighted average of the four test scores, first you need to know each test score and its weight. Next, you multiply each test score with its weight, and then add these numbers to get the average. Therefore,

```
1.  Get testScore1, weightTestScore1
2.  Get testScore2, weightTestScore2
3.  Get testScore3, weightTestScore3
4.  Get testScore4, weightTestScore4
5.  weightedAverage = testScore1 * weightTestScore1 +
                     testScore2 * weightTestScore2 +
                     testScore3 * weightTestScore3 +
                     testScore4 * weightTestScore4;
```
