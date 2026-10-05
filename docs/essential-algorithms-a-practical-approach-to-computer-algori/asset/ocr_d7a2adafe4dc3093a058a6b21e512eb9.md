# Chapter 1 Algorithm Basics

```
b = remainder
End While

// GCD(a, 0) is a.
Return a
End Gcd
```

# THE MOD OPERATOR

The modulus operator, is written Mod in the pseudocode, means the remainder after division. For example, 13 Mod 4 is 1 because 13 divided by 4 is 3 with a remainder of 1.

The equation 13 Mod 4 is usually pronounced "13 mod 4" or "13 modulo 4."

The pseudocode starts with a comment. Comments begin with the characters // and extend to the end of the line.
The first actual line of code is the algorithm's declaration. This algorithm is called GCD and returns an integer. It takes two parameters named a and b, which are integers.

> NOTE Chunks of code that perform a task, optionally returning a result, are variously classed routines, subroutines, procedures, subprocedures, and functions.

The code after the declaration is indented to show that it is part of the method.
The first line in the method's body begins a While loop. The code indented below the While statement is executed as long as the condition in the While statement returns true.
The While loop ends with an End While statement. This statement is not strictly necessary, because the indentation shows where the loop ends, but it provides a reminder of what kind of block statements consists.
The method exits at the Return statement. This algorithm returns a value, so this Return statement indicates which value the algorithm should return. If the algorithm doesn't return any value, such as if its purpose is to arrange values or build a data structure, the Return statement isn't followed by a returned value.
The code in this example is fairly close to actual programming code. Other examples may contain instructions or values described in English. In those cases, the instructions are enclosed in brackets (<>) to indicate that you need to translate the English instructions into program code.

Normally when a parameter or variable is declared (the GCD algorithm, this includes the parameters a and b and the variable (remainder), its data type is given before, followed by a colon, as in Integer: remainder. The data type may be omitted for simple integer looping variables, as in For i = 1 To 10.