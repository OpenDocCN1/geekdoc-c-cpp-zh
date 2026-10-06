```
return 0;
}
```

# Program 13.12. Output

Q Q
/ /
((

The character variable c is defined and initialized to the character 'Q'. In the next line of the program, the variable charPtr is defined to be of type "pointer to char," meaning that whatever value is stored inside this variable should be treated as an indirect reference (pointer) to a character. Notice that you can assign an initial value to this variable in the normal fashion. The value you assign to charPtr in the program is a pointer to the variable c, which is obtained by applying the address operator to the variable c. (Note that this initialization would have generated a compiler error had c been defined after this statement because a variable must always be declared before its value can be referenced in an expression.)

The declaration of the variable charPtr and the assignment of its initial value could have been equivalently expressed in two separate statements, as follows

```
char *charPtr;
charPtr = &c;
```

(and not by the statements

```
*charPtr;
*charPtr = &c;
```

as might be implied from the single line declaration.