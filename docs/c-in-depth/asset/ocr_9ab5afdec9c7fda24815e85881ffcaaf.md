```
#define PRINT3(message) printf(#message);
main()
{
    PRINT1("If we rest, we rust.\n")
    PRINT2("If we rest, we rust.\n")
    PRINT3("If we rest, we rust.\n")
}
```

```
(19)#define show(value) printf ( #value " = %d\n", value);
main()
{
    int a=10,b=5,c=4;
    show(a/b*c);
}
```

```
(20)#define MACRO(a) if(a<=5) printf(#a" = %d\n",a);
main()
{
    int x=6,y=15;
    if(x<=y)
        MACRO(x);
    else
        MACRO(y);
}
```

```
(21)main()
{
    #line 100 "system.c"
    printf("%d %s\n",__LINE__,__FILE__);
}
```

# Answers

+   1. This program will show errors since there is a semicolon after 5, and due to this after expansion the printf statement looks like this- printf(" %d ", 5;)
+   2. If you lapse, don't collapse
+   3. There is a space between the macro name PROD and left parenthesis, so after macro expansion the printf statement looks like this:
+      printf("Product of a and b = %d", (x, y) ( )(x)*(y) )(a, b) );
+      Therefore the program gives error that x and y are undefined symbols.
+   4. i = 55, j = 550
+      The values are calculated as : i = A+100/20; j = 500-A+100;
+   5. When you have a chance
+      to embrace an opportunity
+      Give it a big hug
+   6. 5 4 3 2 1
+   7. 4 3 2 1