**4.2** See the answers below:

+   a) **False.** The default case is optional. If no default action is needed, then there's no need for a default case.
+   
+   b) **False.** The break statement is used to exit the switch statement. The break statement is not required in *any* case.
+   
+   c) **False.** Both of the relational expressions must be *true* for the entire expression to be *true* when using the && operator.
+   
+   d) **True.**

**4.3** See the answers below:

```
a) int sum = 0;
   for (int count = 1; count <= 99; count += 2) {
       sum += count;
   }

b) printf("%-15.1f\n", 333.546372); // prints 333.5
   printf("%-15.2f\n", 333.546372); // prints 333.55
   printf("%-15.3f\n", 333.546372); // prints 333.546
   printf("%-15.4f\n", 333.546372); // prints 333.5464
   printf("%-15.5f\n", 333.546372); // prints 333.54637

c) printf("%10.2f\n", pow(2.5, 3)); // prints 15.63
```

```
d) int x = 1;

   while (x <= 20) {
       printf("%d", x);
       if (x % 5 == 0) {
           puts("");
       }
       else {
           printf("%s", "\t");
       }
       ++x;
   }
```

or

```
int x = 1;
while (x <= 20) {
    if (x % 5 == 0) {
        printf("%d\n", x++);
    }
    else {
        printf("%d\t", x++);
    }
}
```