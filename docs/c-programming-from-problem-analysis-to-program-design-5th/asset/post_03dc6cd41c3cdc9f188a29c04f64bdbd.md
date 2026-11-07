
- 26. Consider the following declaration:

```
template <class type>
class strange
{
    .
    .
    .

private:
    type a;
    type b;
};
```

  - a. Write a statement that declares sObj to be an object of type strange such that the private member variables a and b are of type int.
  - b. Write a statement that shows the declaration in the class strange to overload the operator == as a member function.
  - c. Assume that two objects of type strange are equal if their corresponding member variables are equal. Write the definition of the function operator== for the class strange, which is overloaded as a member function.

- 27. Consider the definition of the following function template:

```
template <class Type>
Type surprise(Type x, Type y)
{
    return x + y;
}
```

What is the output of the following statements?

  - a. `cout << surprise(5, 7) << endl;`
  - b. `string str1 = "Sunny";`
    `string str2 = "Day";`
    `cout << surprise(str1, str2) << endl;`

- 28. Consider the definition of the following function template:

```
template <class Type>
Type funcExp(Type list[], int size)
{
    int j;
    Type x = list[0];
    Type y = list[size - 1];

    for (j = 1; j < (size - 1)/2; j++)
    {
        if (x < list[j])
            x = list[j];
        if (y > list[size - 1 - j])
            y = list[size - 1 - j];
    }

    return x + y;
}
```

Further suppose that you have the following declarations:

```
int list[10] = {5, 3, 2, 10, 4, 19, 45, 13, 61, 11};
string strList[] = {"One", "One", "Three",
                    "How", "Six"};
```

What is the output of the following statements?

  - a. `cout << funcExp(list, 10);`
  - b. `cout << funcExp(strList, 6) << endl;`

- 29. Write the definition of the function template that swaps the contents of two variables.

- 30.
  - a. Overload the operator + for the class `newString` to perform string concatenation. For example, if `s1` is "Hello " and `s2` is "there", the statement:

```
s3 = s1 + s2;
```

should assign "Hello there" to `s3`, in which `s1`, `s2`, and `s3` are `newString` objects.

  - b. Overload the operator += for the class `newString` to perform the following string concatenation. Suppose that `s1` is "Hello " and `s2` is "there". Then, the statement:

```
s1 += s2;
```

should assign "Hello there" to `s1`, in which `s1` and `s2` are `newString` objects.

## PROGRAMMING EXERCISES

- 1.
  - a. Write the definitions of the functions to overload the increment, decrement, arithmetic, and relational operators as members of the class `rectangleType`.
  - b. Write a test program that tests various operations on the class `rectangleType`.

- 2.
  - a. Write the definitions of the functions to overload the increment, decrement, arithmetic, and relational operators as nonmembers of the class `rectangleType`.
  - b. Write a test program that tests various operations on the class `rectangleType`.

- 3.
  - a. Extend the definition of the class `clockType` by overloading the post-increment operator function as a member of the class `clockType`.
  - b. Write the definition of the function to overload the post-increment operator for the class `clockType` as defined in part a.

- 4. a. The increment and relational operators in the `class clockType` are overloaded as member functions. Rewrite the definition of the `class clockType` so that these operators are overloaded as nonmember functions. Also, overload the post-increment operator for the `class clockType` as a nonmember.
  - b. Write the definitions of the member functions of the `class clockType` as designed in part a.
  - c. Write a test program that tests various operations on the class as designed in parts a and b.

- 5. a. Extend the definition of the `class complexType` so that it performs the subtraction and division operations. Overload the operators subtraction and division for this class as member functions.

  If (a, b) and (c, d) are complex numbers:

  (a, b) - (c, d) = (a - c, b - d).

  If (c, d) is nonzero:

  (a, b) / (c, d) = ((ac + bd) / (c² + d²), (-ad + bc) / (c² + d²)).

  - b. Write the definitions of the functions to overload the operators - and / as defined in part a.
  - c. Write a test program that tests various operations on the `class complexType`. Format your answer with two decimal places.

- 6. a. Rewrite the definition of the `class complexType` so that the arithmetic and relational operators are overloaded as nonmember functions.
  - b. Write the definitions of the member functions of the `class complexType` as designed in part a.
  - c. Write a test program that tests various operations on the `class complexType` as designed in parts a and b. Format your answer with two decimal places.

- 7. a. Extend the definition of the `class newString` as follows:
    - i. Overload the operators + and += to perform the string concatenation operations.
    - ii. Add the function length to return the length of the string.
  - b. Write the definition of the function to implement the operations defined in part a.
  - c. Write a test program to test various operations on the `newString` objects.

- 8. a. Rewrite the definition of the `class newString` as defined and extended in Programming Exercise 7 so that the relational operators are overloaded as nonmember functions.
  - b. Write the definition of the `class newString` as designed in part a.
  - c. Write a test program that tests various operations on the `class newString`.

- 9. Rational fractions are of the form $a / b$, in which $a$ and $b$ are integers and $b \ne 0$. In this exercise, by “fractions” we mean rational fractions. Suppose $a / b$ and $c / d$ are fractions. Arithmetic operations on fractions are defined by the following rules:

$a / b + c / d = (ad + bc) / bd$

$a / b - c / d = (ad - bc) / bd$

$a / b \times c / d = ac / bd$

$(a / b) / (c / d) = ad / bc$, in which $c / d \ne 0$.

Fractions are compared as follows: $a / b$ op $c / d$ if $ad$ op $bc$, in which op is any of the relational operators. For example, $a / b < c / d$ if $ad < bc$.

Design a class—say, `fractionType`—that performs the arithmetic and relational operations on fractions. Overload the arithmetic and relational operators so that the appropriate symbols can be used to perform the operation. Also, overload the stream insertion and stream extraction operators for easy input and output.

Write a C++ program that, using the class `fractionType`, performs operations on fractions.

Among other things, test the following: Suppose x, y, and z are objects of type `fractionType`. If the input is 2/3, the statement:

```
cin >> x;
```

should store 2/3 in x. The statement:

```
cout << x + y << endl;
```

should output the value of x + y in fraction form. The statement:

```
z = x + y;
```

should store the sum of x and y in z in fraction form. Your answer need not be in the lowest terms.

- 10. Recall that in C++, there is no check on an array index out of bounds. However, during program execution, an array index out of bounds can cause serious problems. Also, in C++, the array index starts at 0.

Design and implement the class `myArray` that solves the array index out of bounds problem and also allows the user to begin the array index starting at any integer, positive or negative. Every object of type `myArray` is an array of type `int`. During execution, when accessing an array component, if the index is out of bounds, the program must terminate with an appropriate error message. Consider the following statements:

```
myArray<int> list(5);              //Line 1
myArray<int> myList(2, 13);        //Line 2
myArray<int> yourList(-5, 9);      //Line 3
```

The statement in Line 1 declares list to be an array of 5 components, the component type is int, and the components are: list[0], list[1], . . . , list[4]; the statement in Line 2 declares myList to be an array of 11 components, the component type is int, and the components are: myList[2], myList[3], . . . , myList[12]; the statement in Line 3 declares yourList to be an array of 14 components, the component type is int, and the components are: yourList[-5], yourList[-4], . . . , yourList[0], . . . , yourList[8]. Write a program to test the class myArray.

- 11. Programming Exercise 10 processes only int arrays. Redesign the class myArray using class templates so that the class can be used in any application that requires arrays to process data.

- 12. Design a class to perform various matrix operations. A matrix is a set of numbers arranged in rows and columns. Therefore, every element of a matrix has a row position and a column position. If A is a matrix of five rows and six columns, we say that the matrix A is of the size 5 × 6 and sometimes denote it as A_{5×6}. Clearly, a convenient place to store a matrix is in a two-dimensional array. Two matrices can be added and subtracted if they have the same size. Suppose A = [a_{ij}] and B = [b_{ij}] are two matrices of the size m × n, in which a_{ij} denotes the element of A in the ith row and the jth column, and so on. The sum and difference of A and B are given by:

A + B = [a_{ij} + b_{ij}]

A - B = [a_{ij} - b_{ij}]

The multiplication of A and B (A * B) is defined only if the number of columns of A is the same as the number of rows of B. If A is of the size m × n and B is of the size n × t, then A * B = [c_{ik}] is of the size m × t and the element c_{ik} is given by the formula:

c_{ik} = a_{i1}b_{1k} + a_{i2}b_{2k} + · · · + a_{in}b_{nk}

Design and implement a class matrixType that can store a matrix of any size. Overload the operators +, -, and * to perform the addition, subtraction, and multiplication operations, respectively, and overload the operator << to output a matrix. Also, write a test program to test various operations on the matrices.

- 13. a. In Programming Exercise 1 in Chapter 12, we defined a class romanType to implement Roman numbers in a program. In that exercise, we also implemented a function, romanToDecimal, to con-
