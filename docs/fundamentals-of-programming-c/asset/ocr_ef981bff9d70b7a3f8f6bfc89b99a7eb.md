# 9.7 SUMMARY

```
0: Expected 0, but computed 0.0078125
0.0001: Expected 0.01, but computed 0.0116755
0.0008: Expected 0.0282843, but computed 0.0298389
0.0009: Expected 0.03, but computed 0.0313164
0.001: Expected 0.0316228, but computed 0.0327453
```

shows that our square root function produces results of main's acceptable tolerance for few values. Five wrong answers out of one billion tests represents a 0.000005% error rate. This error rate is very small, our square_root function is not perfect. One of values that causes the function to fail may very important to a particular application, so our function is not trustworthy.

# 9.7 Summary

+   - The development of larger, more complex programs is more manageable when the program consists of multiple programmer-defined functions.

+   - Every function has one definition but can have many invocations.

+   - A function definition includes the function's name, parameters, return type, and body.

+   - A function name, like a variable name, is an identifier.

+   - Formal parameters are the parameters as they appear in a function's definition; actual parameters are the arguments supplied by the caller.

+   - Formal parameters are essentially local to the function; actual parameters may be variables, expressions, or literal values.

+   - The values of the actual parameters are copied into the formal parameters when a function is invoked.

+   - Callers pass values to the number of parameters specified in the function definition. The types of the actual parameters must be compatible with the types of the formal parameters.

+   - With C++s default call-by-value parameter passing mechanism, modifying a formal parameter within a function will not affect the value of the caller's actual parameter. The formal parameter is simply a copy of the caller's actual parameter.

+   - Variables declared within a function are local to that function definition. Local variables can not be seen outside the function definition.

+   - During a program's execution, local variables live only when the function is executing. When a particular function is finished, the space allocated for its local variables is freed up.

+   - Programmers should supply comments for each function indicating its purpose and the role(s) of its parameter(s) and return value. Additional information about the function's author, date of last modification, and other information may be required in some situations.