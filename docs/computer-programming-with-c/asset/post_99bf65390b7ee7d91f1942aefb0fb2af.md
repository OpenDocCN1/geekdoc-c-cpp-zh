
This means that the first element of the array can be accessed as `a[0]`, the second element of the array can be accessed as `a[1]` and so on. The last element of the array can be accessed as `a[7]`. Also, every element of the array a will be of type character and it can be initialized using the following statements:

```
a[0] = 'c';
a[1] = 'o';
a[2] = 'm';
a[3] = 'p';
a[4] = 'u';
a[5] = 't';
a[6] = 'e';
a[7] = 'r';
```

Figure 6.19 shows the structure of array a in computer memory.

![](img/57c0d966bb33c67a5a188e6bf39e4e02_254_0.png)

The elements of the array can now be individually processed in the program similar to any other array.

C/C++ also supports an **alternative approach to initialize array of characters as a string constant**. A string constant is always surrounded by double quotes. For example, the following is the valid notation to create a string constant:

```
"computer"
```

We can directly initialize a character array with a string constant as shown in the statement below. In this case, there is no need to specify the size of the array explicitly because the compiler derives the size of the array as **the number of characters in the string + 1**. This is because in the case of **string** initialization the end of the string is marked by the compiler by adding an additional character called NULL CHARACTER (`\0`) as the last character of the array, as shown in Figure 6.20.

```
char a[] = "computer";
```

This means that `a[0]` will be initialized to character value ‘c’, `a[1]` will be initialized to character value ‘o’ and so on, as shown in Figure 6.20.

![](img/57c0d966bb33c67a5a188e6bf39e4e02_254_1.png)

## CAUTION

Directly initializing an array of characters using a string constant is possible only at the time of creating an array. For example, the following approach will not work.

```
char a[9];
a="computer"; /*Error cannot apply string initialization after creation
of an array*/
```

## NOTES

If you need to, you can always specify the size of character array explicitly even if you are initializing it with string constant. For example, the following statement will work well.

But note that you have to specify the size as **number of characters in the string+1**. Remember that additional space of 1 character is consumed for storing NULL character (`\0`) at the end. Anyways, C/C++ does not make it mandatory for the programmer to specify the size of an array when initializing it with string constant. Hence it is best not to specify the size as shown below.

```
char a[] ="computer"; /*Specifying size is optional for string
initialization*/
```

## NOTES

Figure 6.19 shows character by character initialization of an array a. In this case, `\0` will not be added automatically because we are initializing each of the array elements individually. Whereas, Figure 6.20 shows a string initialization of array a, where the compiler automatically adds a NULL character at the end of the array. Hence the size of the array shown in Figure 6.20 is one byte more than the size of the array in Figure 6.19, although the data contents in both the cases are exactly the same.

As a NULL character is automatically added as an end-of-string marker in the case of string initialization, Input/Output functions can correctly identify the position where the string ends. Hence, if we want to print the complete character array a we can write a single `printf()` statement as shown below:

```
printf("%s",a);
```

This statement will print all the characters stored in the array a from the first character up to the NULL character. Hence, the output of the `printf()` statement will be as shown below:

```
computer
```

Remember that `\0` does not appear at the output because it is an internal escape sequence used by the language. Such a direct Input/Output is not possible with any other type of array because C/C++ adds an end marker only with strings. Similar to direct output we can also take a string value to be initialized into an array of characters directly as input from the user. The code below creates a character array b and illustrates the usage of direct Input/Output with the character array.

```c
#include<stdio.h>
void main()
{
char b[100];
printf("Enter a String:\n");
scanf("%s",b);
printf("String is %s \n",b);
}
```

## NOTES

Format specifier `%s` is used while inputting or outputting a string. In this case, we are using `%s` because b is a string type to be taken as input from the user and printed on the computer screen. Needless to say, if you use pure C++ object-oriented style of input and output (using `cin` and `cout` statements) you need not specify any of the format specifiers. Hence the above program can be rewritten using `cin` and `cout` statements without using any of the format specifiers as shown below.

```cpp
#include<iostream.h>
void main()
{
char b[100];
cout<<"Enter a String:"<<endl;
cin>>b;
cout<<"String is "<<b<<endl;
}
```

Recall from Chapter 2 that we must include iostream.h when using objects `cin` and `cout`. Also we can use modifier `endl` instead of `\n` to transfer the cursor to the new line as mentioned in Chapter 2.

The first statement

```c
char b[100];
```

creates an array of characters b of size 100 as shown in Figure 6.21.

![](img/57c0d966bb33c67a5a188e6bf39e4e02_256_0.png)

**Figure 6.21:** Creating an array b

We can directly take the string to be stored inside an array b as input from the user using a statement

```c
scanf("%s",b);
```

because C/C++ supports direct input and output operations with an array of characters. Note that there is no need to specify the ampersand symbol in `scanf()` statement while taking a string as input from the user. This is because strings in C/C++ are self-addressable. We will revisit the concept of self-addressability in Chapter 7 so do not worry about it right now, but for now just remember not to specify ampersand symbols when inputting strings using `scanf()` statement.

Let us assume that the user inputs a string as `Hello`, this will be stored in array b starting from position 0 as shown in Figure 6.22. Also, note that an end-of-the-string marker `\0` (NULL character) will be automatically stored at position 5 of the array to represent the end, because this is a string input done using `%s`, as shown in Figure 6.22.

![](img/57c0d966bb33c67a5a188e6bf39e4e02_257_0.png)

The statement

```cpp
printf("String is %s \n",b);
```

will print all the characters in string b from position 0 up to the NULL character. Note that the NULL character will not appear at the output. Hence, output on the computer screen will be as follows:

```text
Hello
```

> **What is the advantage of NULL character getting added at the end of the string?**
>
> We know that NULL character is added to an array when we input the array in string mode (using `%s`) or when we directly initialize it using a string constant. One of the advantages of NULL character is that we can perform direct Input and Output operations with the array, due to its presence. When we perform direct input or direct initialization of an array with a string constant, C/C++ automatically adds `\0` at the end of the string. And, when we print an array (say `a`) using the statement:
>
> ```cpp
> printf("%s",a);
> ```
>
> This will print all the valid elements of the array because the `printf()` function knows the exact point when the string ends due to the presence of `\0`.

![](img/57c0d966bb33c67a5a188e6bf39e4e02_259_0.png)

**Figure 6.24:** Calculating length of string

incremented to 1 to compare the next character stored in `a[1]` with '\0'; the execution of the for loop proceeds similarly for all the subsequent iterations. Note that the for loop terminates when the value of variable `i` is 4 because `a[4]` is storing '\0' and hence the value of variable `len` is incremented exactly three times as shown in Figure 6.24. Therefore, the value of `len` will always reflect the length of the string in `a`. In this case, variable `len` is set to 3 at the end of the loop because there are three characters in the string `hat`.
