```
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
```

# NOTES

Format specifier %s is used while inputting or outputting a string. In this case, we are using %s because b is a string type to be taken as input from the user and printed on the computer screen. Needless to say that, if you use pure C++ object oriented style of input and output (using cin and cout statements) you need not specify any of the format specifiers. Hence the above program can be rewritten using cin and cout statements without using any of the format specifiers as shown below.

```
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
```

Recall from Chapter 2 that we must include iostream.h when using objects cin and cout. Also we can use modifier endl instead of \n to transfer the cursor to the new line as mentioned in Chapter 2.

The first statement

```
```c
char b[100];
```
```

creates an array of characters b of size 100 as shown in Figure 6.21.

![](bbox=[0.153, 0.647, 0.827, 0.769])

**Figure 6.21:** Creating an array b

We can directly take the string to be stored inside an array b as input from the user using a statement

```
```c
scanf("%s",b);
```
```

because C/C++ supports direct input and output operations with an array of characters. Note that there is no need to specify ampersand symbol in scanf() statement while taking