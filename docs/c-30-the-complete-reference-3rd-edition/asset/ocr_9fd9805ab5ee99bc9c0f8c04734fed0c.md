The assignment operator does have one interesting attribute that you may not be familiar with: It allows you to create a chain of assignments. For example, consider this fragment:

```
```
int x, y, z;

x = y = z = 100; // set x, y, and z to 100
```
```

This fragment sets the variables x, y, and z to 100 using a single statement. This works because the = is an operator that yields the assigned value. Thus, the value of z = 100 is 100, which is then assigned to y, which in turn is assigned to x. Using a “chain of assignment” is an easy way to set a group of variables to a common value.

# ## Compound Assignments

C# provides special compound assignment operators that simplify the coding of certain assignment statements. Let’s begin with an example. The assignment statement shown here:

```
```
x = x + 10;
```
```

can be written using a compound assignment as

```
```
x += 10;
```
```

The operator pair += tells the compiler to assign to x the value of x plus 10.

Here is another example. The statement

```
```
x = x - 100;
```
```

is the same as

```
```
x -= 100;
```
```

Both statements assign to x the value of x minus 100.

There are compound assignment operators for many of the binary operators (that is, those that require two operands). The general form of the shorthand is

*var-name* *op* = *expression*;

Thus, the arithmetic and logical assignment operators are

| += | -= | *= | /= |
| --- | --- | --- | --- |
| %= | &= | \|= | ^= |

Because the compound assignment statements are shorter than their noncompound equivalents, the compound assignment operators are also sometimes called the *shorthand assignment operators*.

The compound assignment operators provide two benefits. First, they are more compact than their “longhand” equivalents. Second, they can result in more efficient executable code (because the left-hand operand is evaluated only once). For these reasons, you will often see the compound assignment operators used in professionally written C# programs.