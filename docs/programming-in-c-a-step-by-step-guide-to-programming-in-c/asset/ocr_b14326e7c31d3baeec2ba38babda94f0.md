any precedence rules or parentheses for unique definition. So, evaluation of a postfix expression is possible using a stack-based algorithm.

# Program 14.4: Program to convert an infix expression to prefix form #include <stdio.h>

```
#include <string.h>
#include <ctype.h>
#define N 80
typedef enum {FALSE, TRUE} bool;
#include "stack.h"
#include "queue.h"
#define NOPS 7

char operators [] = "() / ^ * + -";
int priorities[] = {4,4,3,2,2,1,1};
char associates[] = "RLLLLL";

char t[N]; char *tptr = t; // this is where prefix will be saved.
int getIndex( char op ) {
/*
*returns index of op in operators.
*/
int i;
for( i=0; i<NOPS; ++i )
if( operators[i] == op )
```