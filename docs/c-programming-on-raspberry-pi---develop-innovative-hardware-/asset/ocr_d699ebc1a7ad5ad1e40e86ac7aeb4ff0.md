An example run of the program is shown in Figure 3.22.

```
```text
How many students are there?: 4
Enter age of student 1 :23
Enter age of student 2 :35
Enter age of student 3 :32
Enter age of student 4 :28
Maximum age = 35
pi@raspberrypi:~ $
```
```

Figure 3.22 Example run of the program

# ### 3.2.9 ● String variables

It is important in every programming language to be able to manipulate text and characters. In C, text strings are represented as arrays of characters, where the first character is stored in index 0. The array is terminated with the NULL character ('\0') which is the ASCII 0. A string declaration is shown below:

```
```c
char name[] = "John";
```
```

Notice it is not necessary to specify the length of the string as this is calculated by the compiler. The above statement creates a character array having 5 elements including the NULL character at the end. The characters are stored in the array as shown below:

| 0 | 1 | 2 | 3 | 4 |
|---|---|---|---|---|
| J | o | h | n | '\0' |

We can also specify the array size as:

```
```c
char name[10] = "John";
```
```

Notice the specified array size is greater than the number of elements in the array. Here, the compiler allocates additional space at the end of the array so extra text can be appended in the future. The keyword **BUFSIZ** can be used when an array is declared if the length of the array is not known. **BUFSIZ** sets the array size to the maximum value allowed by the compiler.

The name of an array is also its address in memory. Therefore, when it is required to enter the address of an array, we can simply enter its name, or specify its address by using the & sign in front of its first element. e.g. as &name[0].

Strings can be printed using the %s qualifier of the printf example as shown in the following example.