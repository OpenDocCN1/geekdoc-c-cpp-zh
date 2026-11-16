Note that if the string is not enclosed in double quotes, the compiler will not display the message. If the set-of-characters for a macro is longer than one line, a backslash (\\ ) character must be placed at the end of the line indicating that the set-of-characters continues on the next line. For example,

```
#define Two_line_string "This is a two line\\ string"
```

The identifier or the macro name can have arguments. Each time the identifier is encountered, the arguments used in the macro name are replaced by the actual arguments found in the program. This type of macro is called as the function macro. Program 2.20, helps you to understand things better.

# Program 2.20:

```
/* macro3.c */
#define PI 3.14159
#define AREA_OF_CIRCLE(R) (PI*R*R)
void main()
{
    float radius, area;
    printf("Enter the radius of the circle : ");
    scanf("%f", &radius);
    area = AREA_OF_CIRCLE(radius);
    printf("The area of the circle is %4f", area);
}
```

The program displays the following output
Enter the radius of the circle : 4
The area of the circle is 50.2654

wherever AREA_OF_CIRCLE(radius) appears in the program, the value of radius is substituted for R in the set-of-characters, the symbolic constant PI is replaced by its value (i.e., PI is replaced by 3.14159) and the macro is expanded in the program. For example, the statements

```
area = AREA_OF_CIRCLE(4);
```

is expanded as

```
area = ( 3.14159*4*4 );
```

and the program evaluates the area of the circle and displays the message. Symbolic constants and macros can be undefined using the #undef preprocessor directive. The general form or the syntax of #undef directive is

```
#undef identifier
```

where identifier is the already defined macro name.

The scope of a symbolic constant or macro is from its definition (i.e., from #define) upto or until it is undefined using #undef directive. After the #undef directives, any references made to the corresponding identifiers will be ignored. For example,