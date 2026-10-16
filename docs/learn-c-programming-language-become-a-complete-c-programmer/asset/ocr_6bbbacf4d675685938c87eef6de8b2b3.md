expression denoting the object to be incremented is evaluated once (only). Decrementing is similarly expressed by the-- operator.

The operators ++ and-- can be used as both prefix and postfix operators. The value of ++x is the new (that is, incremented) value of x. For example, y=++x is equivalent to y=(x=x+1). The value of x++, however, is the old value of x. For example, y=x++ is equivalent to y=(t=x,x=x+1,t), where t is a variable of the same type as x.

Like adding an int to a pointer, or subtracting it, ++ and-- on a pointer operate in terms of elements of the array into which the pointer points; p++ makes p point to the next element (§7.4.1).

The ++ and-- operators are particularly useful for incrementing and decrementing variables in loops. For example, one can copy a zero-terminated C-style string like this:

```
void cpy(char* p, const char* q)
{
while (*p++ = *q++);
}
```

Like C, C++ is both loved and hated for enabling such terse, expression-oriented coding. Consider: while (*p++ = *q++);

This is more than a little obscure to non-C programmers, but because the style of coding is not uncommon, it is worth examining more closely. Consider first a more traditional way of copying an array of characters:

```
int length = strlen(q);
for (int i = 0; i<=length; i++)
p[i] = q[i];
```

This is wasteful. The length of a zero-terminated string is found by reading the string looking for the terminating zero. Thus, we read the string twice: once to find its length and once to copy it. So we try this instead:

```
int i;
for (i = 0; q[i]!=0 ; i++)
p[i] = q[i];
p[i] = 0; // terminatingzero
```

The variable i used for indexing can be eliminated because p and q are pointers:

```
while ( *q!=0){
*p= *q;
p++; // point to next character
q++; // point to next character
}
*p=0; // terminatingzero
```

Because the post-increment operation allows us first to use the value and then to increment it, we can rewrite the loop like this:

Section 11.1.4 Increment and Decrement 277