with the same meaning, can only be used in one program (and in the subprograms/macros nested to it). So, if a calculated value in one program is needed to be used in other program(s) also, it has to be stored in a permanent common variable (i.e., #500 to #999).

A permanent common variable always has the same meaning for all the programs, not only in the current machining session, but also in all future sessions, until it is modified to store a new value. And, it can be modified anytime by any program. It can also be modified in the MDI mode. It is not cleared by the M02/M30/RESET button.

Although not recommended (in the interest of a safe programming practice, as most of the people believe that the local variables and the common variables in a new program start with null values), the following parameter setting would retain the values stored in local and common variables, even after system reset (though power OFF will still clear them):

+   - `Parameter 6001#6 = 1` — Retains common variables even after system reset
+   - `Parameter 6001#7 = 1` — Retains local variables even after system reset

The default setting for these parameter bits is 0, which clears the stored values, if any, whenever the system is reset. It is, however, good programming practice not to depend on defaults and set all the local and common variables to null before using them in a program. And, the permanent common variables also should be carefully used because they may contain some previously stored values.

# 3.3 Levels of Local Variables

A macro always starts with null values for all the local variables, except those whose values are passed on to the macro through the arguments of the macro call. The method of passing desired values to certain local variables is discussed in detail in Chap. 7. At this stage, it is sufficient to know that G65 P2 A5 is a macro call for program number 2, with macro variable #1 = 5 (initially), and the other local variables of the macro running null.

The local variables, defined in a macro, remain accordingly defined only in the current call of the macro. Any subsequent call of the same macro will again start with null values for all the local variables (except, of course, those defined through the argument list):

```
Main program

O0001;                 (Program number 1)
G65 P2 A5;             (The macro execution starts with #1 = 5, and sets
                       #10 = 5. Then, it redefines #1 and stores 6 in it.
                       Other local variables of the macro remain null.
                       Once the execution of the macro is complete, the
                       values assigned to #1 and #10 are lost)
```