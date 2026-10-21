# 1. Use of #define Directive

#define preprocessor directive can be used to declare a constant. It's general syntax is given as :

```
#define constant_name value
```

There must be at least a single space between #define and constant_name. For example : #define PI 3.14 which declares a constant (actually it is a macro constant) named PI with value 3.14. There should be no assignment operator (=) between PI and 3.14. Each macro constant must be declared on separate line. Macro constants are also known as symbolic constant as we use string symbols to define constants.

```
/*PROG 3.26 DEMO OF CONSTANT #DEFINE*/

#define PI 3.14
#define H "hello"
#define DMC "Demo of macro constant"
#include <iostream.h>
void main()
{
cout << H << endl;
cout << DMC << endl;
cout << "The value of PI" << PI << endl;
}
OUTPUT :
hello
Demo of macro constant
The value of PI3.14
```

![](bbox=[0.33, 0.63, 0.71, 0.74])

Figure 3.26. Output screen of program.

EXPLANATION : We have used three symbolic constants in the program named PI, H and DMC. First one (PI) is a float constant and other two are string constants. Before compilation they are processed by a special program called preprocessor which replaces all the occurrences of macro constant by their value. Each macro constant is return in upper case, it is not necessary but to distinguish macro name from variables we declare macro in upper-case and variables in lower-case.