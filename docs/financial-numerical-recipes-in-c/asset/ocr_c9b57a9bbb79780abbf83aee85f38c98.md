```
>> A=[1 2 3;4 5 6]
A =
1 2 3
4 5 6
```

Observe that when filling in a vector or a matrix a space or a comma means a new number, a semicolon a new row. To suppress the printing of what you just defined, end the line with a semicolon:

```
>> A=[1,2,3,4];
>> A=[1,2,3,4]
A =
1 2 3 4
>>
```

You can also use defined variables to define new variables, as long as the dimensions make sense. For example, given the above definitions:

```
>>B=[c x]
B =
3 1 2 3
C = 1 2 3
>> C = [A;x]
C =
1 2 3
4 5 6
1 2 3
>> D = [A y]
error: number of rows must match
error: evaluating assignment expression near line 22, column 3
```

If dimensioning is wrong, you get an error message, and the variable is not defined. To see what is in a variable, tell Matlab to print the value by giving the name:

```
>> a
a = 1
>> A
A =
1 2 3
4 5 6
```

Note that Matlab is case-sensitive, both A and a are defined.

# 2.2.2 Arithmetic Matrix Operations.

We now get to the important parts of Matlab, namely, its built-in matrix arithmetic. Given the definitions above, let us add and subtract a few elements according to the rules of matrix algebra. We first show how to manipulate numbers and vectors:

```
>> a=1
a = 1
>> b=2
b = 2
>> a+b
ans = 3
```