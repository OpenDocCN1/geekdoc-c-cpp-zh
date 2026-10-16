i The integer argument is converted to decimal notation;
o The integer argument is converted to octal notation;
x The integer argument is converted to hexadecimal notation;
X The integer argument is converted to hexadecimal notation;
f The float or double argument is converted to decimal notation in the style [−]ddd.ddd. The number of d’s after the decimal point is equal to the precision for the argument. If necessary, the number is rounded. If the precision is missing, six digits are given; if the precision is explicitly 0 and # isn’t specified, no decimal point is printed;
F Like %f but uses capital letters for INF, INFINITY, and NAN.
e The float or double argument is converted to decimal notation in the scientific style [−]d.ddd e+dd or [−]d.ddd e−dd, where there is one digit before the decimal point and the number of digits after the decimal point is equal to the precision specification for the argument. If necessary, the number is rounded. If the precision is missing, six digits are given; if the precision is explicitly 0 and # isn’t specified, no digits and no decimal point are printed;
E As e, but with an uppercase E used to identify the exponent;
g The float or double argument is printed in style d, in style f, or in style e, whichever gives the greatest precision in minimum space;
G As g, but with an uppercase E used to identify the exponent;
a The double argument is printed in the hexadecimal format [−]0xh.hhhh p+d or [−]0xh.hhhh p+d;
A Like %a but using X and P instead or x and p;
c The character argument is printed. Null characters are ignored;
s The argument is taken to be a string (character pointer), and characters from the string are printed until a null character or until the number of characters indicated by the precision specification is reached; however, if the precision is 0 or missing, all characters up to a null are printed;
p The argument is taken to be a pointer. The representation printed is implementation dependent;
u The unsigned integer argument is converted to decimal notation;
n The number of characters written so far by the call of printf(), fprintf(), or sprintf() is written to the int pointed to by the pointer to int argument.
In no case does a nonexistent or small field width cause truncation of a field; padding takes place only if the specified field width exceeds the actual width.
Here is a more elaborate example:
char * line_format = "#line %d "%s"\n";
int line = 13;
char* file_name = "C++/main.c";
printf("int a;\n");
printf(line_format,line ,file_name);
which produces:
int a;
#line 13 "C++/main.c"
Using printf() is unsafe in the sense that type checking is not done. For example, here is a