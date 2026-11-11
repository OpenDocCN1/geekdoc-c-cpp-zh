# TEST YOUR KNOWLEDGE

Q6. Rewrite the following ‘do’ loop into a ‘while’ loop.

```
```cpp
int n=1;
float x=0;
float s;
do
{
  s=1.0/(n*n);
  x=x+s;
  n++;
}
while(s>0.01);
```
```

Ans. The following changes are made to convert ‘do’ loop into a ‘while’ loop:

```
```cpp
int n=1;
float x=0;
float s=1.0;
while(s>0.01)
{
  s=1.0/(n*n);
  x=x+s;
  n++;
}
```
```

# Using the for Loop

The for-loop iterates over a fixed number of times and consists of three parts, such as initialization, conditional expression, and post expression. The following is the syntax of the for-loop:

```
```cpp
for(initialization;conditional_expression;post_expression)
```
```

In the preceding syntax, the initialization initializes the variable with a value. The initialization part occurs once, which is followed by the conditional expression. If the conditional expression evaluates to false, then the statement following the for-loop is evaluated. If the conditional_expression evaluates to true, then the body of the for-loop is executed. The post_expression is used to increment or decrement a counter variable controlling a loop. The for-loop continues to execute until the conditional_expression evaluates to false. Listing 23 shows the use of the for-loop (you can find this example in the forloop.cpp file on the CD in the code\chapter2 folder):

# ▶ Listing 23: Using the for Loop

```
```cpp
#include<iostream.h>
```
```