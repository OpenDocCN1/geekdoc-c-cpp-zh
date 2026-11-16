```
{
int x = 1;
while (x<=50) ;
{
printf("ERROR") ;
x++;
}
}
```

In the above program the value of x will not be incremented and always remains less than 50. Therefore the program segment should be

```
while (x <= 50)
{
printf("ERROR") ;
x++;
}
```

# 9. Improper comment characters

Every comment should start with a /* and end with a */. Anything between them is ignored by the compiler. If we miss out the opening /* or the closing */ then the compiler searches in the program treating all lines as comments. Hence, we will get an error message. One opening /* should be always accompanied with a closing */. Otherwise, an error will be occurred.

# 10. Undeclared variables

C requires every variable to be declared for its type, before it is used. During the development of a large program, one may use a variable, which has not been declared. Hence, it gives an error.

# 11. Using spaces in between operators

It is a common error to leave spaces in between operators like ==, !=, >=, <=.

# 12. Reversing the order of operators

It is a common error to reverse the order of operators like =!, =>, =<.

# 13. Confusing the precedence of various operators

Expressions are evaluated according to the precedence of operators. It is common among beginners to confuse the precedence of operators.

Example : while(sum=multiply() <= 50)
sub = 5 - sum;

The function call multiply() returns the product of three numbers, which is compared to 50. If the value is equal to or less than 50, the relational test is true, and 1 is assigned to sum, otherwise 0 will be assigned. But this is not the output the programmer wanted.

The expression should be

```
while(sum=multiply() <= 50)
sub = 5 - sum;
```