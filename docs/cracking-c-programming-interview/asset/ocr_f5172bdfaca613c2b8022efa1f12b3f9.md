Explanation: Option (a) gives an error because the multiple line macro does not have '\' at the last line.

+   14. b

Explanation: Not required. Hint: The statement at line 2, after macro substitution is: int f = e*a+b*c+d;

+   15. c

Explanation: The line 2, after macro sqrt() substitution become: int y = x++++++x; this expression get evaluated as: y = (x++)+ (x++)*(x+x) → y = (10)+(11)*(13) → y = 153.

Hint: The order of precedence of operators for the given expression is: post increment > pre increment '>' > '+'(lowest among these operator). The post increment gets evaluated on encountering any other operator like '+' and ''.

+   16. b

Explanation: Not required. Hint: After macro substitution 'a' and 'b' become pointer of character type.

+   17. a

Explanation: Not required.

+   18. a

Explanation: Not required. Another version of question 17 with typedef. typedef vs #define

+   1. #define and typedef both are used to define aliases for various data types and values.

+   2. typedef can assign an alias for data types only whereas #define can be used to assign aliases for values also e.g. #define 2 MONDAY

+   3. #define is pre-processor directive and substitutes its aliases at pre-processing time only whereas typedef is resolved during compilation time.

+   4. #define is not bounded by scoping rules, its scope is till the macro or the end of the file or re-define the same macro whereas typedef has scoping rules as as