# Accessing Array Components

The general form (syntax) used for accessing an array component is:

```
`arrayName[indexExp]`
```

in which indexExp, called the **index**, is any expression whose value is a nonnegative integer. The index value specifies the position of the component in the array.

In C++, `[]` is an operator called the **array subscripting operator**. Moreover, in C++, the array index starts at 0.

Consider the following statement:

```
`int list[10];`
```

This statement declares an array list of 10 components. The components are `list[0]`, `list[1]`, ..., `list[9]`. In other words, we have declared 10 variables (see Figure 8-3).

![](bbox=[0.199, 0.456, 0.898, 0.541])

**FIGURE 8-3** Array list

The assignment statement:

```
`list[5] = 34;`
```

stores 34 in `list[5]`, which is the *sixth* component of the array list (see Figure 8-4).

![](bbox=[0.199, 0.687, 0.898, 0.773])

**FIGURE 8-4** Array list after execution of the statement `list[5] = 34;`

Suppose i is an `int` variable. Then, the assignment statement:

```
`list[3] = 63;`
```

is equivalent to the assignment statements:

```
i = 3;
list[i] = 63;
```