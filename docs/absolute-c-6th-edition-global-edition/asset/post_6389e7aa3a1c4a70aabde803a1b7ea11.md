
corresponding argument in a function call can be a variable, but the function takes only the value of the variable and does not change the variable in any way. With a call-by-value formal parameter only the value of the argument is substituted for the formal parameter. For an input function, you want the variable (not the value of the variable) to be substituted for the formal parameter. The call-by-reference mechanism works in just this way. With a call-by-reference formal parameter, the corresponding argument in a function call must be a variable, and this argument variable is substituted for the formal parameter. It is almost as if the argument variable were literally copied into the body of the function definition in place of the formal parameter. After the argument is substituted in, the code in the function body is executed and can change the value of the argument variable.

A call-by-reference parameter must be marked in some way so that the compiler will know it from a call-by-value parameter. The way that you indicate a call-by-reference parameter is to attach the ampersand sign, &, to the end of the type name in the formal parameter list. This is done in both the function declaration (function prototype) and the header of the function definition. For example, the following function definition has one formal parameter, receiver, which is a call-by-reference parameter:

```cpp
void getInput(double& receiver)
{
    cout << "Enter input number:\n";
    cin >> receiver;
}
```

In a program that contains this function definition, the following function call will set the double variable inputNumber equal to a value read from the keyboard:

```cpp
getInput(inputNumber);
```

C++ allows you to place the ampersand either with the type name or with the parameter name, so you will sometimes see

```cpp
void getInput(double &receiver);
```

which is equivalent to

```cpp
void getInput(double& receiver);
```

Display 4.2 demonstrates call-by-reference parameters. The program reads in two numbers and writes the same numbers out, but in the reverse order. The parameters in the functions getNumbers and swapValues are call-by-reference parameters. The input is performed by the function call

```cpp
getNumbers(firstNum, secondNum);
```

The values of the variables firstNum and secondNum are set by this function call. After that, the following function call reverses the values in the two variables firstNum and secondNum:

```cpp
swapValues(firstNum, secondNum);
```

## Display 4.2 Call-by-Reference Parameters

```cpp
1 //Program to demonstrate call-by-reference parameters.
2 #include <iostream>
3 using namespace std;

4 void getNumbers(int& input1, int& input2);
5 //Reads two integers from the keyboard.

6 void swapValues(int& variable1, int& variable2);
7 //Interchanges the values of variable1 and variable2.

8 void showResults(int output1, int output2);
9 //Shows the values of output1 and output2, in that order.

10 int main()
11 {
12     int firstNum, secondNum;

13     getNumbers(firstNum, secondNum);
14     swapValues(firstNum, secondNum);
15     showResults(firstNum, secondNum);
16     return 0;
17 }

18 void getNumbers(int& input1, int& input2)
19 {
20     cout << "Enter two integers: ";
21     cin >> input1
22     >> input2;
23 }

24 void swapValues(int& variable1, int& variable2)
25 {
26     int temp;

27     temp = variable1;
28     variable1 = variable2;
29     variable2 = temp;
30 }

31 void showResults(int output1, int output2)
32 {
33     cout << "In reverse order the numbers are: "
34         << output1 << " " << output2 << endl;
35 }
```

### Sample Dialogue

```text
Enter two integers: 5 6
In reverse order the numbers are: 6 5
```

The next few subsections describe the call-by-reference mechanism in more detail and also explain the particular functions used in Display 4.2.

### Call-by-Reference Parameters

To make a formal parameter a call-by-reference parameter, append the ampersand sign, &, to its type name. The corresponding argument in a call to the function should then be a variable, not a constant or other expression. When the function is called, the corresponding variable argument (not its value) will be substituted for the formal parameter. Any change made to the formal parameter in the function body will be made to the argument variable when the function is called. The exact details of the substitution mechanisms are given in the text of this chapter.

### EXAMPLE

```cpp
void getData(int& firstInput, double& secondInput);
```

### Call-by-Reference Mechanism in Detail

In most situations the call-by-reference mechanism works as if the name of the variable given as the function argument were literally substituted for the call-by-reference formal parameter. However, the process is a bit more subtle than that. In some situations, this subtlety is important, so we need to examine more details of this call-by-reference substitution process.

Program variables are implemented as memory locations. Each memory location has a unique address that is a number. The compiler assigns one memory location to each variable. For example, when the program in Display 4.2 is compiled, the variable firstNum might be assigned location 1010, and the variable secondNum might be assigned 1012. For all practical purposes, these memory locations are the variables.

For example, consider the following function declaration from Display 4.2:

```cpp
void getNumbers(int& input1, int& input2);
```

The call-by-reference formal parameters input1 and input2 are placeholders for the actual arguments used in a function call.

Now consider a function call like the following from the same program:

```cpp
getNumbers(firstNum, secondNum);
```

When the function call is executed, the function is not given the argument names firstNum and secondNum. Instead, it is given a list of the memory locations associated with each name. In this example, the list consists of the locations

```text
1010
1012
```

which are the locations assigned to the argument variables firstNum and secondNum, in that order. It is these memory locations that are associated with the formal parameters.

The first memory location is associated with the first formal parameter, the second memory location is associated with the second formal parameter, and so forth. Diagrammatically, in this case, the correspondence is

```text
firstNum ⟶ 1010 ⟶ input1
secondNum ⟶ 1012 ⟶ input2
```

When the function statements are executed, whatever the function body says to do to a formal parameter is actually done to the variable in the memory location associated with that formal parameter. In this case, the instructions in the body of the function getNumbers say that a value should be stored in the formal parameter input1 using a cin statement, and so that value is stored in the variable in memory location 1010 (which happens to be the variable firstNum). Similarly, the instructions in the body of the function getNumbers say that another value should then be stored in the formal parameter input2 using a cin statement, and so that value is stored in the variable in memory location 1012 (which happens to be the variable secondNum). Thus, whatever the function instructs the computer to do to input1 and input2 is actually done to the variables firstNum and secondNum.

It may seem that there is an extra level of detail, or at least an extra level of verbiage. If firstNum is the variable with memory location 1010, why do we insist on saying "the variable at memory location 1010" instead of simply saying "firstNum?" This extra level of detail is needed if the arguments and formal parameters contain some confusing coincidence of names. For example, the function getNumbers has formal parameters named input1 and input2. Suppose you want to change the program in Display 4.2 so that it uses the function getNumbers with arguments that are also named input1 and input2, and suppose that you want to do something less than obvious. Suppose you want the first number typed in to be stored in a variable named input2 and the second number typed in to be stored in the variable named input1—perhaps because the second number will be processed first or because it is the more important number. Now, let's suppose that the variables input1 and input2, which are declared in the main part of your program, have been assigned memory locations 1014 and 1016. The function call could be as follows:

```cpp
int input1, input2;
getNumbers(input2, input1);
```

Notice the order of the arguments.

In this case if you say "input1," we do not know whether you mean the variable named input1 that is declared in the main part of your program or the formal parameter input1. However, if the variable input1 declared in the main function of your program is assigned memory location 1014, the phrase "the variable at memory location 1014" is unambiguous. Let's go over the details of the substitution mechanisms in this case.

In this call the argument corresponding to the formal parameter input1 is the variable input2, and the argument corresponding to the formal parameter input2 is the variable input1. This can be confusing to us, but it produces no problem at all for the computer, since the computer never does actually "substitute input2 for input1" or "substitute input1 for input2." The computer simply deals with memory locations. The computer substitutes "the variable at memory location 1016" for the
