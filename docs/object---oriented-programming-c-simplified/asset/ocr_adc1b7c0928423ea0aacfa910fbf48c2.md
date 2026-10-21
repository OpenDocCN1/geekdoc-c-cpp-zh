![](bbox=[0.26, 0.14, 0.74, 0.36])

# Figure 15.5. Output screen of program.

EXPLANATION : We have overloaded all the 4 binary operation viz +, -, * and /. You can check that code for all the overloaded operation function is same except for the operator symbol. In the division operator function we have checked for denominator to be nonzero. Note overloading of operator does not change their inherent meaning, priority and associativity. So the expression d5 = d1 + d2 * d3 / d1 - d4; is evaluated as (assuming num for objects as shown in the program output) :

As priority of * and / is higher than + and – and at the same level of priority * and / are evaluated from left to right so d2 *d3 is evaluated first which internally interpreted as d2.operator * (d3) as explained earlier. Assuming the returned object as temp1 with value of num96 (as 8 *12=96) the expression becomes d5 = d1+temp1/d1-d4. Now temp / d1 will be evaluated where temp1 calling the function operator / and sending d1 as argument. Assuming returned object as temp2 with value of num is 19.2 (as 96/5 = 19.2) the expression becomes d5 = d1 + temp2 – d4. As priority of + and – is same expression will be evaluated from left to right so next d1 +temp2 will be evaluated where d1 calling the operator function + and sending temp2 as argument. Assuming the returned object as temp3 with value of num 24.2 (as 19.2 + 5 = 24.2) the expression becomes d5=temp3-d4. Now temp3 calls the operator function – and sends d4 as argument. Assuming the returned object as temp4 with value of num 15.2 (as 24.2-9) the expression becomes d5=temp4 and value of num will be assigned to num to object d5.

```
/* PROGRAM : OVERLOADING PRE ++ AND POST ++ IN THE SAME PROGRAM */

#include <iostream.h>
#include <conio.h>

class demo
{
    int num;
public :
    demo() {}
```