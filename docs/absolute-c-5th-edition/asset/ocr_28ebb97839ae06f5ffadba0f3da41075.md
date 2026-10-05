The next few subsections describe the call-by-reference mechanism in more detail and also explain the particular functions used in Display 4.2.

# # Call-by-Reference Parameters

To make a formal parameter a call-by-reference parameter, append the ampersand sign, & to its name. The corresponding argument in a call to the function should then be a variable, not a constant or other expression. When the function is called, the corresponding argument (not its value) will be substituted for the formal parameter. Any change made to the formal parameter in the function body will be made to the argument variable when the function is called. The exact details of the substitution mechanisms are given in the text of this chapter.

EXAMPLE

```
void getData(int& firstInput, double& secondInput);
```

# # Call-by-Reference Mechanism in Detail

In situations the call-by-reference mechanism works as if the name of the variable given as the function argument were literally substituted for the call-by-reference formal parameter. However, the process is more subtle than that. In some situations, this subtlety is important, so we examine more details of this call-by-reference substitution process.

Program variables are implemented as memory locations. Each memory location has a unique address that is a number. The compiler assigns one memory location to each variable. For example, when the program in Display 4.2 is compiled, the firstNum might be assigned location 1010, and the secondNum might be assigned 1012. For all practical purposes, these memory locations are the variables. For example, consider the following function declaration from Display 4.2:

```
void getNumbers(int& input1, int& input2);
```

The call-by-reference formal parameters input1 and input2 are placeholders for the actual arguments used in a function. Now consider a function call like the following from the same program:

```
getNumbers(firstNum, secondNum);
```

When the function is executed, the function is not given the argument names firstNum and secondNum. Instead, it is given a list of the memory locations associated with each name. In this example, the list consists of the locations

+   - 1010
- 1012

which are the locations assigned to the argument variables firstNum and secondNum, in that order. It is memory locations that are associated with the formal parameters.