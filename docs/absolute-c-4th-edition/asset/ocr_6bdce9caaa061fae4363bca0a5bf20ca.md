# Display 4.2  Call-by-Reference Parameters (part 2 of 2)

# SAMPLE DIALOGUE

```
Enter two integers: 5 6
In reverse order the numbers are: 6 5
```

the functions getNumbers and swapValues are call-by-reference parameters. The input is performed by the function call

```
getNumbers(firstNum, secondNum);
```

The values of the variables firstNum and secondNum are set by this function call. After that, the following function call reverses the values in the two variables firstNum and secondNum:

```
swapValues(firstNum, secondNum);
```

The next few subsections describe the call-by-reference mechanism in more detail and also explain the particular functions used in Display 4.2.

# CALL-BY-REFERENCE PARAMETERS

To make a formal parameter a call-by-reference parameter, append the ampersand sign, &, to its type name. The corresponding argument in a call to the function should then be a variable, not a constant or other expression. When the function is called, the corresponding variable argument (not its value) will be substituted for the formal parameter. Any change made to the formal parameter in the function body will be made to the argument variable when the function is called. The exact details of the substitution mechanisms are given in the text of this chapter.

# EXAMPLE

```
void getData(int& firstInput, double& secondInput);
```

# CALL-BY-REFERENCE MECHANISM IN DETAIL

In most situations the call-by-reference mechanism works as if the name of the variable given as the function argument were literally substituted for the call-by-reference formal parameter. However, the process is a bit more subtle than that. In some situations, this subtlety is important, so we need to examine more details of this call-by-reference substitution process.