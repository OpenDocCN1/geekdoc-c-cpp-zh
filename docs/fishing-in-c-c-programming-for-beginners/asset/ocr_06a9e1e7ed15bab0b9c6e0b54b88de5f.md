compiler to subtract the displayed result from the original result and the answer is non zero. This experiment proves an amazing fact about the compiler that, a compiler can display something other than whatever it has stored. This experiment confirms the fact that a variable cannot show any number of digits after the decimal point rather it has a limit. The limit is:

A variable shows only six digits of any number assigned to it excluding the decimal point and exponential symbols; if the number of digits increases after the decimal point then the compiler starts rounding the number and if the number of digits increases before decimal point then the compiler round the first six digits and expresses it in scientific form, but the compiler performs any mathematical calculations from the original digits assigned to it without rounding each number and as soon as the final result is obtained, it rounds the final number to six digits while displaying it but may not round it in memory.

I call this rule as Variable constraint. We have to keep this rule in mind for various calculations. This rule is applicable to all the input and output operations even including calculations.

# Difference between declarations and definitions:

Now, time has come where we should learn the difference between a declaration and a definition.

# Declarations

A declaration is any statement which occupies the memory but it has not been assigned any value. E.g. following statements are declarations:

```
```
int num;
```
```

```
```
char ch1,ch2,ch3;
```
```

```
```
void fact();
```
```

Here, the function has been declared only, not defined. If you will try to use this function, it will give an error “undefined reference to fact()”

e.g. following program will not run and give the above error:

```
```
#include<iostream>
```
```

```
```
using namespace std;
```
```

```
```
void fact();
```
```

```
```
int main()
```
```