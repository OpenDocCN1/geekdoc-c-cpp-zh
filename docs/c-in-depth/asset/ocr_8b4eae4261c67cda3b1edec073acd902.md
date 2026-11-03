Now a call SHOW(x); will be expanded as printf("x" "=%d", x); We know that adjacent strings are concatenated so after string concatenation this becomes- printf("x = %d", x); We can make the above macro more general so that it can display variable of any type.

```
/*P12.12 Program to understand the use of stringizing operator*/
#include<stdio.h>
#define SHOW(var,format) printf(#var " = %" #format "\n",var);
main()
{
    int x=9;float y=2.5;char z='$';
    SHOW(x,d);
    SHOW(y,0.2f);
    SHOW(z,c);
    SHOW(x*y,0.2f);
}
```

# Output:

x = 9
y = 2.50
z = $
x*y = 22.50

The macros in the above program were expanded as-
SHOW(x, d);  → printf("x" " = %" "d" "\n", x);
SHOW(y, 0.2f );  → printf("y" " = %" "0.2f" "\n", y);
SHOW(z, c);  → printf("z" " = %" "c" "\n", z);
SHOW(x*y, 0.2f);  → printf("x*y" " = %" "0.2f" "\n", x*y);

After string concatenation the above statements look like this-
printf("x = %d\n", x);
printf("y = %0.2f \n", y);
printf("z = %c\n", z);
printf("x*y = %0.2f \n", x*y);

# 12.9 Token Pasting Operator(## )

Token pasting operator ## is used in a macro definition to concatenate two tokens into a single tok
As the name implies, this operator pastes the two token into one.

```
/*P12.13 Program to understand the use of token pasting operator*/
#include<stdio.h>
#define PASTE(a, b) a##b
#define MARKS(subject) marks_##subject
main()
{
    int k2=14,k3=25;
```