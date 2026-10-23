# Template

# Objective

+   - Defining template
+   - Scenario of templates
+   - Usage of template
+   - Creation of template
+   - Discussing the prominent examples.

# INTRODUCTION

Templates are used for creating the generic class and function. It is recently added features in C++. Templates offer the following advantages:

+   - Avoids re-writing of the code.
+   - Eliminates the testing of re-written code.
+   - Prevents any error that may creep due to re-writing of the code.

Aforementioned reasons are among the various reasons due to which templates have gained the wide popularity. We can understand the limitations that exist due to non-usage of template with the help of following sub-sections.

# NEED OF A TEMPLATE

Consider a case in which user is intending to initialize the integer in a function call. Similarly, same array size is used to inititialize the float members. In each case argument is passed in a function depending upon the type of data. Consequently, to accomplish this objective, (s) he has to define the following program.

```
#include<iostream.h>
#include<conio.h>
const int size=4;
class one
{
int a [size];
float b [size];
public:
one (int []);
one (float []);
```