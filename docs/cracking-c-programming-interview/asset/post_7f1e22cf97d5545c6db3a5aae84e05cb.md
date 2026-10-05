
and default (if it's there) will execute until the break is encountered
or the end of the switch.

+   21. c
    - gcc: garbage, garbage
    - turboC: 700, 500
    - **Explanation**: It is a compiler-dependent program.

+   22. d
    - **Explanation**: The *case* label must be a constant or constant expression. The variable/non-constant expression is not allowed in the case label. The enumerated type can also be used as a case label statement.

+   23. c
    - **Explanation**: As we discussed in the above explanation, the constant expressions are allowed as a *case* label. Here, the error is due to duplication in the case label.

+   24. c
    - **Explanation**: The variable 'i' is visible to the inside block only. But we can access its value through address out of the block because the lifetime of the address of a block in a main exists till the exit of the main function.

+   25. c
    - **Explanation**: The variable 'p' is a constant integer and stored in a read-only memory area. Its value cannot be updated. In our program, we are updating the value of 'p' at line 2. Hence, the compiler will throw an error.

+   26. b
    - **Explanation**: In the gcc compiler, the lexical (phase of compilation) scanning of symbols starts from left to right. The operator (++, +, -, ++) which comes first will be treated as the first symbol. Here, i++j can be treated in two ways, either (i++)+j or i+(++j). The first operator is '+' which comes in lexical scanning but after '+', the '+' symbol again encounters and now the first operator becomes '++'. It associates the '++' operator with i, the second operator is '+', which is a binary operator and applied to both operands. The second way of expressing the given expression i+(++)j) is discarded.

+   27. d
Explanation: The compiler will throw an error at line 5, sizeof('*p') and '*q' are not known due to their void nature. If we typecasting of 'p' and 'q' to any data type pointer, like *(int *)p and *(int*) q, it will work fine.

+   28. b
Explanation: The same version of this program is already discussed in the explanation of question 10.

+   29. c
Explanation: The void pointer is a generic pointer type, arithmetic operations are not allowed on void pointers. The void pointers are generally used for passing void pointers to functions, after passing function, type conversion can be done. The void pointers are also referred to as intermediate pointer types. (check explanation of question 3 and question 4).

+   30. c
Explanation: The scanf returns the total number of valid inputs accepted by it, and printf returns the number of characters printed by it on the display. In a given program, scanf is taking two valid integer inputs, so 'q' is 2 and inside printf will print "India" and return 5. Outside printf will print 2+5 i.e. 7. Hence, the output will be "India7".

+   31. d
Explanation: The scanf returns 0 if the non-formatted value is entered as input. In a given program we are formatting scanf with '%d' at line 2. So, scanf is expecting integer type value, with integer value, "while" will become infinite loop "while(1)", if character or any other data type value is given, scanf will return 0, and while loop will get terminated.

+   32. a- true, b- true, c- false, d- false
Explanation: Not required.

+   33. b
Explanation: The extern is just as a declaration and expect the definition of the variable later in the program (linking phase). Its resolution takes place during the scanning of symbols, and symbol table creation. The extern specifies that the definition for the extern type variable is present in some other programs/library or in the same program as a global variable. The given program compiles correctly but when the resolution of ‘p’ comes, it checks in other associated files, library files for the definition of variable ‘p’. But it would not find any definition of ‘p’ because it is just a variable name, not any keyword. Linker link-time error gets thrown by the compiler. Linker Error : Undefined symbol ‘p’.

+   34. b
Explanation: The ‘p’ is not an external variable, so the compiler will check from the symbol table and throws an error that ‘p’ is not declared. If we use extern it means that compiler skips and waits the linking phase for resolving p.

+   35. a
Explanation: It works fine, the resolution of ‘p’ will not take place at compile-time, it takes place during link time. The definition of ‘p’ is present in the symbol table. Hence, the value of ‘p’ can be directly resolved during link time.

+   36. d
Explanation: It's a concept of the void pointer, we already discussed it in explanation of questions 3, 4, 29.

+   37. d
Explanation: One more flavor of switch statement we have discussed in the explanation of questions 20 and 22.

+   38. d
Explanation: A simple recursive program, explanation not required.

+   39. c

+   40. c
Explanation: The printf returns the number of characters printed. Here, printf is accepting a zero-length string "", hence it returns 0. The output will be "India is great".
Explanation: A simple program with few while loops, explanation not required.

+   41. a
Explanation: Default decimal number is double in C. We know double is more precise, so float f may hold 0.69999999 which is less than 0.7. Hence "India" gets printed. For real numbers like float, double, and long double the exact value cannot be predicted.
Note: Be cautious when comparing floating numbers with relational operators as '=', '>', '<', '=', '>=', etc.

+   42. c
Explanation: The compiler throws an error due to the continue statement. The continue can only be used in loops.

+   43. c
Explanation: The assignment operator is right to left associative. It returns the right-hand side evaluated expression.
Given Expression i = (j = 4) can be evaluated as; i = 4; Since, (j=4) returns 4.

+   44. c
Explanation: The continue statement skips all the subsequent statements inside the loop and start execution from the beginning of the loop. The break statement skips all the subsequent statements inside the loop and control goes out of the loop.

+   45. c
Explanation:
pre increment:
```
x = ++i; can be decomposed into two statements:
```
```
i = i+1;
```
```
x = i;
```
post increment:
y = i++; can be decomposed into two statements:
y = i;
i = i+1;

+   46. d Explanation: The precedence of the relational operator is more than the assignment '=' operator. Hence, the resolution of '>' happens first, x > y returns 1; if 'x' is greater than 'y', else 0. See precedence table in "A touch to C" chapter.

+   47. 1, -1, 0, 1, -1, -1, -2, 1, -3, 1, -4, 1, -5, 1 Explanation: The expression j = -5<i--; can be written in two steps: (i) j = -5<i; (ii) i--; Now it is easy to get answer for the program.

+   48. c Explanation: The preprocessor substitutes 'v,a,r' in main(). The macro symbol is used to concatenate with 'v,a,r'.

+   49. c Explanation: The comma operator has left-to-right associativity. L-R associativity, left is evaluated then right, 3, 7, 9. So 3, 7, 10.

+   50. d Explanation: In gcc and Turbo C the function call passes parameters from right to left, the given program outputs option b. And for online compiler it can give option c.

+   51. b printf("%s ", &ch[8]-&ch[2] + ch);→ 1009-1003=1006 printf("%s",1006);

# Output: India
The behavior of %s has been discussed in question 8.
Explanation: ch[] = "Hello India";

| 'H' | 'e' | 'l' | 'l' | 'o' | ' ' | 'I' | 'n' | 'd' | 'i' | 'a' | '0' |
|---|---|---|---|---|---|---|---|---|---|---|---|
| 1000 | 1002 | 1003 | 1004 | 1005 | 1006 | 1007 | 1008 | 1009 | 1010 | 1011 | 1012 |

```
ch 1000
&ch[2]
&ch[8]
```

Figure 2.6: Representation of memory allocation of string in stack area

+   52. b
Explanation: As we know that in the standard C compiler the real constant value has double data type by default but if suffixed any real number with 'f' like .4f, it becomes equivalent to 0.399999 in float format.

+   53. a
Explanation: The macros can also be used with the function name.

+   54. d
Explanation: Take care of global, local variables and precedence of operators in function P().

+   55. b
Explanation: If global variables are not initialized, they automatically get initialized with 0.

+   56. a
Explanation:
```
'c' and 'd' both hold the address of variable 'a' of main(). Whatever modifiers applied on 'c' and 'd', the same impact will get reflected on 'a'.
*c = *c + (*d + 2); *1000 = *1000 + (*1000 + 2)
*d = *d * (*c - 3); *1000 = *1000 * (*1000 - 3)
```

Figure 2.7: Pointer representation in stack area

+   57. a
