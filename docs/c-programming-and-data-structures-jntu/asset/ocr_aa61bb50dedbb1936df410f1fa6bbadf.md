+   3. '# ' must be the first character in the line.
+   4. A blank space is required between #define and symbolic name and between the symbolic name and the constant.
+   5. #define statements must not end with a semicolon.
+   6. After definition, the symbolic name should not be assigned any other value within the program by using an assignment statement. For example, STRENGTH = 200; is illegal.
+   7. Symbolic names are NOT declared for data types. Its data type depends on the type of constant.
+   8. #define statements may appear anywhere in the program but before it is referenced in the program (the usual practice is to place them in the beginning of the program).

#define statement is a preprocessor compiler directive and is much more powerful than what has been mentioned here. More advanced types of definitions will be discussed later. Table 3.11 illustrates some invalid statements of #define.

# Table 3.11 Examples of Invalid #define Statements

| Statement | Validity | Remark |
|---|---|---|
| #define X = 2.5 | Invalid | '=' sign is not allowed |
| #define MAX 10 | Invalid | No white space between # and define |
| #define N 25; | Invalid | No semicolon at the end |
| #define N 5, M 10 | Invalid | A statement can define only one name. |
| #Define ARRAY 11 | Invalid | define should be in a lowercase letters |
| #define PRICE$ 100 | Invalid | $ symbol is not permitted in name |

# CASE STUDIES

# 1. Calculation of Average of Numbers

A program to calculate the average of a set of N numbers is given in Fig. 3.9.

```
Program
/***********************************************************/
/*              AVERAGE OF n VALUES                        */
/**********************************************************/

#define  N  10                 /* SYMBOLIC CONSTANT */

main()
{
    int    count;              /* DECLARATION OF */
    float  sum, average, number;   /* VARIABLES */

    sum = 0;                   /* INITIALIZATION */
    count = 0;                 /* OF VARIABLES */
    while (count < N)
    {
```