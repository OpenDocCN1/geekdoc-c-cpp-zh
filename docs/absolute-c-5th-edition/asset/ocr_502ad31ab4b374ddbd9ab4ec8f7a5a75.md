The first memory location is associated with the first formal parameter, the second memory location is associated with the second formal parameter, and so forth. Diagrammatically, in this case, the correspondence is

```
firstNum      ---> 1010 ---> input1
secondNum    ---> 1012 ---> input2
```

When the functions are executed, whatever the memory function says to a formal parameter is actually done to the variable in the memory location associated with that parameter. In this case, the instructions of the function getNumbers input using a value that should be stored in the formal parameter input1010 (which happens to be the variable firstNum). Similarly, the instructions in the function getNumbers input2 using a c statement, and that value should be stored in the variable in memory location 1012 (which happens to be the variable secondNum). Thus, whatever the function instructs the computer to do to input1 and input2 is actually done to the variables firstNum and secondNum.

It may seem that extra level of detail, or at least another level of verbiage. If firstNum is variable with memory location 1010, why do we insist on saying "the variable at memory location 1010" instead of saying "firstNum?" This extra level of detail is needed if the arguments and formal parameters contain confusing indices of names. For example, the function getNumbers has parameters input1 and input2. Suppose you want to change the program in Display 4.2 so that it uses the function getNumbers with arguments that are named input1 and input2, and suppose you want to do something less than obvious. Suppose you want the first number typed to be stored in a variable named input1—because the second number will be processed first or because it is more important number. Now, let's suppose that the variables input1 and input2, which are declared in the main part of your program, have been assigned memory locations 1014 and 1016. The function could call as follows:

```
input1, input2;
getNumbers(input2, input1);
```

In this case if you say "input", we do not know whether the variable input1 is declared in the main part of your program or the formal parameter input1. However, if the variable input1 declared in the main function of your program is assigned memory location 1014, the phrase "the variable at memory location 1014" is unambiguous. Let's go over the detail of the substitution mechanisms in this case.

In this call the argument concerning the formal parameter input1 is the variable input2, and the argument corresponding to the formal parameter input2 is the variable input1. This can be confusing but it produces no problem at all for the computer, since the computer never does actually "substitute input2 for input1" or "substitute input1 for input2." The computer simply deals with memory locations. The computer substitutes "the variable at memory location 1016" for the