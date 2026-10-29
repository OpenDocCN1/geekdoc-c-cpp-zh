this reason, a program outline with stubs is usually the most efficient method of testing. A common approach is to use driver programs to test some basic functions, such as input and output, and then use a program with stubs to test the remaining functions. The stubs are replaced by functions one at a time: One stub is replaced by a complete function and tested; once that function is fully tested, another stub is replaced by a full function definition, and so forth, until the final program is produced.

# THE FUNDAMENTAL RULE FOR TESTING FUNCTIONS

Every function should be tested in a program in which every other function in that program has already been fully tested and debugged.

# Self-Test Exercises

+   11. What is the fundamental rule for testing functions? Why is this a good way to test functions?
+   12. What is a driver program?
+   13. What is a stub?
+   14. Write a stub for the function whose declaration is given below. Do not write a whole program, only the stub that would go in a program. *(Hint: It will be very short.)*

```
double rainProb(double pressure, double humidity, double temp);
//Precondition: pressure is the barometric pressure in inches of mercury,
//humidity is the relative humidity as a percentage, and
//temp is the temperature in degrees Fahrenheit.
//Returns the probability of rain, which is a number between 0 and 1.
//0 means no chance of rain. 1 means rain is 100% certain.)
```

# Chapter Summary

+   • A formal parameter is a kind of placeholder that is filled in with a function argument when the function is called. In C++, there are two methods of performing this substitution, call by value and call by reference, and so there are two basic kinds of parameters: call-by-value parameters and call-by-reference parameters.
+   • A call-by-value formal parameter is a local variable that is initialized to the value of its corresponding argument when the function is called. Occasionally, it is useful to use a formal call-by-value parameter as a local variable.
+   • In the call-by-reference substitution mechanism, the argument should be a variable, and the entire variable is substituted for the corresponding argument.