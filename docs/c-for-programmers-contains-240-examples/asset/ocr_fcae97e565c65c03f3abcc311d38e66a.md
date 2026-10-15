```
global x in main is 1
local x in main's outer scope is 5
local x in main's inner scope is 7
local x in main's outer scope is 5

local x is 25 on entering useLocal
local x is 26 on exiting useLocal

local static x is 50 on entering useStaticLocal
local static x is 51 on exiting useStaticLocal

global x is 1 on entering useGlobal
global x is 10 on exiting useGlobal

local x is 25 on entering useLocal
local x is 26 on exiting useLocal

local static x is 51 on entering useStaticLocal
local static x is 52 on exiting useStaticLocal

global x is 10 on entering useGlobal
global x is 100 on exiting useGlobal

local x in main is 5
```

Fig. 6.11 | Scoping example. (Part 3 of 3.)

To demonstrate other scopes, the program defines three functions, each of which takes no arguments and returns nothing. Function useLocal (lines 41–48) declares automatic variable x (line 43) and initializes it to 25. When the program calls useLocal, the function prints the variable, increments it and prints it again before the function returns program control to its caller. Each time the program calls this function, the function recreates automatic variable x and reinitializes it to 25.

Function useStaticLocal (lines 53–62) declares static variable x and initializes it to 50. Local variables declared as static retain their values even when they are out of scope (i.e., the function in which they are declared is not executing). When the program calls useStaticLocal, the function prints x, increments it and prints it again before the function returns program control to its caller. In the next call to this function, static local variable x contains the value 51. The initialization in line 55 occurs only once—the first time useStaticLocal is called.

Function useGlobal (lines 65–70) does not declare any variables. Therefore, when it refers to variable x, the global x (line 11, preceding main) is used. When the program calls useGlobal, the function prints the global variable x, multiplies it by 10 and prints it again before the function returns program control to its caller. The next time the program calls useGlobal, the global variable has its modified value, 10. After executing functions useLocal, useStaticLocal and useGlobal twice each, the program prints the local variable x in main again to show that none of the function calls modified the value of x in main, because the functions all referred to variables in other scopes.

# 6.11 Function Call Stack and Activation Records

To understand how C++ performs function calls, consider a data structure (i.e., collection of related data items) known as a stack. Stacks are last-in, first-out (LIFO) data structures—the last item pushed (inserted) on the stack is the first item popped (removed) from it.