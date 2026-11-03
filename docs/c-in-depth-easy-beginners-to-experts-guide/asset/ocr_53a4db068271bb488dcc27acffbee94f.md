might have been set up.

#incude<conio.h>: This command would look for the file conio.h in the specified list of directories only.

# 2. Indicate what would the swap macro be expanded to on preprocessing. Would the code compile?

```
#define swap (a, b, c) (c t; t=a; a=b; b=t)
main()
{
    int x=10,y=20;
    swap (x, y, int);
    printf("%d %d",x,y);
}
```

Answer: (int t;t=a,a=b,b=t);

This code will not work since declaration of t cannot occur within parenthesis.

# 3. How would you modify the swap macro in the above question such that it is able to interchange two integers?

Answer: #define swap(a,b,c) c t;t=a, a=b, b=t;

# 4. In which line of the following program an error would be reported?

+   1. #define area( r ) (3.14*r *r);
+   2. main()
+   3. {
+   4.     float r=1.0, c;
+   5.     c=area(r);
+   6.     printf("%f",c);
+   7.     if(area(r) = =6.28)
+   8.         printf("Matrix");
+   9. }

Answer: Line number 7, but the real culprit is the semicolon in the line number 1. On expansion line number 7 becomes if((3.14*1.0*1.0); = =6.28). Hence the error.