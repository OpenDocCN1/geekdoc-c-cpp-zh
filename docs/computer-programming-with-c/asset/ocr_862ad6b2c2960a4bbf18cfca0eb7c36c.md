```
```c
for(i=0;i<=2;i++)
{
    scanf("%d%s%s%f", &b[0].id,b[0].title,b[0].author,&b[0].price);
}
```
```

Figure 9.14 shows the final state of an array assuming sample input data.

![](bbox=[0.188, 0.224, 0.815, 0.426])

**Figure 9.14:** State of objects b[0], b[1], and b[2] after user input

In general, we can access a member of iᵗʰ Book object in b by using the following statement:

```
```c
b[i].<memberName>;
```
```

Following for loop will print the details of each of the Book objects on the computer screen:

```
```c
for(i=0;i<=2;i++)
{
    printf("%d\t%s\t%s\t%f\n", b[i].id, b[i].title, b[i].author, b[i].
        price);
}
```
```

When counter variable i takes a value 0, the **printf()** statement will print the id, title, author, and price of object b[0], whereas when the value of i is incremented to 1 the **printf()** statement will print the id, title, author, and price of object b[1] and so on. As the size of the array is 3, we terminate the for loop when the value of index variable i crosses 2. This is because the last Book object will be stored at position 2 as shown in the Figure 9.14. Therefore, the output of the given for loop will be as shown below:

```
```text
1  C++      Kunal 900
2  Java     Jack  800
3  Fortran  Jill  400
```
```

The following is the full source code which creates an array of type Book of size 3, accepts the details about each book as input from the user and prints them back on the computer screen.

```
```c
#include<stdio.h>
struct Book
```
```