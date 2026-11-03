# ***Else Statements***

Another way to handle an either or decision, is to use the keyword *else*. Take a look at the code below:

```
````c
1 #include <stdio.h>
3 int main()
4 {
5 int a;
6
7 printf("Type an integer: ");
8 scanf("%d", &a);
9 printf("You otyped %d.\n",a);
10 if(a > 10)
11 {
12  printf("%d is greater than 10.\n",a); 13 }
14 else
15 {
16  printf("%d is less than or equal to 10.\n",a); 17 }
18
19 return(0);
20 }
21
````
```

This code is a rewrite of our previous code, but it uses the *else* keyword. The *if* condition at line 10 makes an evaluation. Its statements are executed when that condition is true. If the