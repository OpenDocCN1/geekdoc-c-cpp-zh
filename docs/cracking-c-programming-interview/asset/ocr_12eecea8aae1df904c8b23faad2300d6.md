Hence, c[0] = 5; c[1] = 0; c[2] = 0; c[8] = 7;

**Figure 3.6:** Representation of an array element in hexadecimal in Big Endian mode

The expression, char *c = (char *)a; char pointer can only access one byte at a time. Now the step size of accessing a byte becomes 1, while storing the step size was 4B integer value.

+   26. **c**
Explanation: The execution of a given program is done in two steps: (i) The macro FOO(x) will get substituted as foo(#x), where '#' converts 'x' to string. The number 65 will be converted into the string "65". (ii) The function call will take place as foo("65"). In function(), string "65" is pointed by character pointer 'x'. Hence, x[0] will give '6' and x[1] will give '5'.

+   27. **c**
Explanation: A program can have the same function name and variable name in different scopes, the given question will print 3. Suppose if we make "int main = 3;" as global variable, then the program would have thrown an error as "int main = 3;" and "int main()" both become global, and are in same scope.

+   28. **b**
Explanation: The curly braces after the case 1 statement will never execute, as it is out of the scope of the case.

+   29. **d**
Explanation: The switch statement can only support type "integer", "character", "short", "long" and enum. Floating-point data types are not allowed with the switch statement.

+   30. **Invalid- a; valid- b, c, d;**
Explanation: Not required.

+   31. **d**
Explanation: ‘else’ without ‘if’ is not allowed. Hence, the compiler throws an error.

+   32. **c**
Explanation: In the given program all instances of strnc(x, y) will be substituted by x = y, the preprocessed program will not have