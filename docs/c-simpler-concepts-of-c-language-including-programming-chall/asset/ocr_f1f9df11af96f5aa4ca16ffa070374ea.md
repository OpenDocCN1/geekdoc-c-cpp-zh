g→ for enabling global optimizations.

s ort→for specifying short or fast sequences of machine code.

y→ for generating frame pointers on the program stack.

For example, #pragma optimize("qty", on)

2. #pragma warning(disable:<warning>)

Using this, warnings are suppressed. For example, consider the following piece of code, where the pragma is used to suppress warnings with initializations.#pragma warning(disable:4700) will do this job, so the line 4 ‘int y=x’ will produce any error. In the next line, the warning is enabled using #pragma(default:4700). Hence, warning occurs on executing 2nd line in main(). (Note that these directives are platform dependant. And so, results will be varying from platform to platform.)

```
#pragma warning(disable:4700)
void Test() {
int x;
int y = x; // no C4700
#pragma warning(default:4700) // C4700 enabled after Test ends
}
```

```
int main() {
int x;
int y = x; // C4700
}
```

# **Program 14.6 Pragma example**

So, the reader will be familiar with the pre-processor directives now. Try answering questions at the Quiz part for testing.

> POINTS TO REMEMBER

+   - Pre-processor directives are processed before compilation phase.
- File inclusion, macro substitution, Conditional compilation are the 3 main usage of pre-processor directives.
- #define, #ifdef, #include are some of the widely used directives.
- It is not an error to include a same file twice in a program.
- Token pasting operator concatenates the parameters.
- Stringing operator treats the parameter as strings.

# 14.3 QUIZ

+   1. Spot the error in the following code.

```
#include<stdio.h>

#define SWAP(a,b,c) (c temp=a,a=b,b=temp)
int main() {
int x=10,y=20;
SWAP(x,y,int);
printf("%d %d",x,y);
getch();
}
```