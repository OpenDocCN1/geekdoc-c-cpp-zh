ments in C produce a value, namely the value that’s assigned to the variable on the left side of the assignment operator.

For example, suppose we intend to write

```
```c
if (payCode == 4) {
    printf("%s", "You get a bonus!");
}
```
```

but we accidentally write

```
```c
if (payCode = 4) {
    printf("%s", "You get a bonus!");
}
```
```

The first if statement properly awards a bonus to the person whose paycode is equal to 4. The second if statement—the one with the error—evaluates the assignment expression in the if condition. This expression is a simple assignment whose value is the constant 4. Because any nonzero value is interpreted as “true,” the condition in this if statement is always true, and not only is the value of payCode inadvertently set to 4, but the person always receives a bonus regardless of what the actual paycode is.

> **Common Programming Error 4.5**
> 
> Using operator == for assignment or using operator = for equality is a logic error.

# lvalues and rvalues

You’ll probably be inclined to write conditions such as x == 7 with the variable name on the left and the constant on the right. By reversing these terms so that the constant is on the left and the variable name is on the right, as in 7 == x, then if you accidentally replace the == operator with =, you’ll be protected by the compiler. The compiler will treat this as a syntax error, because only a variable name can be placed on the left-hand side of an assignment expression. This will prevent the potential devastation of a runtime logic error.

Variable names are said to be lvalues (for “left values”) because they can be used on the left side of an assignment operator. Constants are said to be rvalues (for “right values”) because they can be used only on the right side of an assignment operator. lvalues can also be used as rvalues, but not vice versa.

> **Error-Prevention Tip 4.8**
> 
> When an equality expression has a variable and a constant, as in x == 7, you may prefer to write it with the constant on the left and the variable name on the right (i.e., 1 == x) as protection against the logic error that occurs when you accidentally replace operator == with =.

# Confusing == and = in Standalone Statements

The other side of the coin can be equally unpleasant. Suppose you want to assign a value to a variable with a simple statement such as

```
```c
x = 1;
```
```

but instead write

```
```c
x == 1;
```
```