variable and then assigning the value to the same variable:

a+=5; is equivalent to a=a+5
a-=5; is equivalent to a=a-5
a*=5; is equivalent to a=a*5
a/=5; is equivalent to a=a/5
a%=5; is equivalent to a=a%5

# 5. Equality operator - ==, !=

These two operators are used to check whether the given expression has the right and left sides equal or not. This operator is also a Boolean operator it also gives answer in 0 or 1.

```
int a,b,c=5;
a==5;
b!=2;
printf("%d, %d",a,b);
```

Output:- 1,0

# 6. Logical Operator - &&, ||, !

These operators are also Boolean operators. && and || operator are used with two expressions. These expressions generally have either relational operators or equality operators in them.

| Expression 1 | Expression 2 | && | || |
|---|---|---|---|
| 0 | 0 | 0 | 0 |
| 1 | 0 | 0 | 1 |
| 0 | 1 | 0 | 1 |
| 1 | 1 | 1 | 1 |

The NOT operator is used to reverse the expression:

| Expression | ! |
|---|---|
| 0 | 1 |
| 1 | 0 |

```
int a=10,b=5,c,d;
c= a>3 && b!=3;
```