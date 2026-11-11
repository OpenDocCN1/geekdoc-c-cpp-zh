```
```c
printf("\n\np = %.12f\np = %.12e", p,q);
}

Output
Values of x and y:12.3456 17.5e-2
x = 12.345600
y = 0.175000
Values of p and q:4.142857142857 18.5678901234567890
p = 4.142857142857
q = 1.856789012346e+001
```
```

*Fig. 6.5* Reading of real numbers

# ### 6.4.3 Inputting Character Strings

We have already seen how a single character can be read from the terminal using the **getchar** function. The same can be achieved using the **scanf** function also. In addition, a **scanf** function can input strings containing more than one character. Following are the specifications for reading character strings:

```
`%ws or %wc`
```

The corresponding argument should be a pointer to a character array. However, %c may be used to read a single character when the argument is a pointer to a **char** variable.

# ## WORKED-OUT PROBLEM 6.6

Reading of strings using **%wc** and **%ws** is illustrated in Fig. 6.6.

The program in Fig. 6.6 illustrates the use of various field specifications for reading strings. When we use **%wc** for reading a string, the system will wait until the w<sup>th</sup> character is keyed in.

**Note** that the specification **%s** terminates reading at the encounter of a blank space. Therefore, **name2** has read only the first part of "New York" and the second part is automatically assigned to **name3**. However, during the second run, the string "New-York" is correctly assigned to **name2**.

```
```c
Program

main()
{
    int no;
    char name1[15], name2[15], name3[15];
    printf("Enter serial number and name one\n");
    scanf("%d %15c", &no, name1);
    printf("%d %15s\n\n", no, name1);
    printf("Enter serial number and name two\n");
    scanf("%d %s", &no, name2);
    printf("%d %15s\n\n", no, name2);
    printf("Enter serial number and name three\n");
    scanf("%d %15s", &no, name3);
}
```
```