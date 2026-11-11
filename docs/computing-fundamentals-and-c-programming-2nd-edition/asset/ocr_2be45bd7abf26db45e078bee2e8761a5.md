```
~~~
1 Rs 11400.00
2 Rs 12996.00
3 Rs 14815.44
4 Rs 16889.60
5 Rs 19254.15
Input amount, Interest rate, and period

20000 0.12 7

1 Rs 22400.00
2 Rs 25088.00
3 Rs 28098.56
4 Rs 31470.39
5 Rs 35246.84
6 Rs 39476.46
7 Rs 44213.63
~~~
```

**Fig. 4.10** *Interactive investment program*

Note that the **scanf** function contains three variables. In such cases, care should be exercised to see that the values entered match the *order* and *type* of the variables in the list. Any mismatch might lead to unexpected results. The compiler may not detect such errors.

# ## 4.11 DEFINING SYMBOLIC CONSTANTS

We often use certain unique constants in a program. These constants may appear repeatedly in a number of places in the program. One example of such a constant is 3.142, representing the value of the mathematical constant “pi”. Another example is the total number of students whose mark-sheets are analysed by a ‘test analysis program’. The number of students, say 50, may be used for calculating the class total, class average, standard deviation, etc. We face two problems in the subsequent use of such programs. These are

+   1. problem in modification of the program and
+   2. problem in understanding the program.

# ### 4.11.1 Modifiability

We may like to change the value of “pi” from 3.142 to 3.14159 to improve the accuracy of calculations or the number 50 to 100 to process the test results of another class. In both the cases, we will have to search throughout the program and explicitly change the value of the constant wherever it has been used. If any value is left unchanged, the program may produce disastrous outputs.

# ### 4.11.2 Understandability

When a numeric value appears in a program, its use is not always clear, especially when the same value means different things in different places. For example, the number 50 may mean the number of students at