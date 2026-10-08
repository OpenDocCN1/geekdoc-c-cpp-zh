Notice that a cast operator is a data type written with parentheses. These changes happen outside the variable's storage in the expressions in which the cast is used. The original declared data type will not change and the value in storage will not change. An int value may be changed to float by the use of mixed-mode arithmetic, for example, var1 + 0.0 or 1.0 * var1, but a float value can only be changed to int by using the cast operator.

sizeof Operator The storage for a variable is allocated in bytes. One byte of storage is required to store a character. In C, the number of bytes of storage allocated to a variable depends on the data type of the variable. At run-time the the sizeof operator determines the number of bytes of storage allocated for a particular variable or a data type. The sizeof operator may also be used to determine the storage allocated for the basic data types of a specific computer. The following examples show the use of the sizeof operator.

To determine the default number of bytes allocated for an int variable on a computer:

```
int var, varsize;
```

```
varsize = sizeof(int);
```

or

```
varsize = sizeof(var);
```

Both statements will assign the same value, which is four, to varsize on most computers.

To determine the default number of bytes allocated for a float variable on a computer:

```
float var;
```

```
int varsize;
```

```
varsize = sizeof(float);
```

or

```
varsize = sizeof(var);
```