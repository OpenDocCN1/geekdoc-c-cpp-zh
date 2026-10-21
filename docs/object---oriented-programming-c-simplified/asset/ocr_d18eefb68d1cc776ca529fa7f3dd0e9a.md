![](bbox=[0.145, 0.132, 0.855, 0.242])

Figure 3.31. Output screen of first and second run of program.

# EXPLANATION :

The priority of % is higher than ==, so a%2 is compared to 0. If this is true then the number is even else number is not even. The else part executes only when if part is false and vice-versa. In the program both if and else part contains just one statement to be dependent upon them so braces are not needed, however if you put there won't be any harm. The condition could be written in the following manner also :

```
if(num%2!=0)
    printf("number is odd\n");
else
    printf("number is even\n");
```

```
/*PROG 3.31 TO CALCULATE GROSS SALARY OF THE PERSON.GIVEN BASIC SALARY(BS) AS INPUT.IF BS IS >5000 DA=55%N OF BS AND HRA=15% BS ELSE DA=45% OF BS AND HRA=10% OF BS*/

#include <iostream.h>
void main()
{
    float bs,gs,hra,da;
    cout<<"Enter your basic salary"<<endl;
    cin>>bs;
    if(bs<=5000)
    {
        da=(bs*45)/100;
        hra=(bs*10)/100;
    }
    else
    {
        da=(bs*55)/100;
        hra=(bs*15)/100;
    }
    gs=bs+da+hra;
    cout<<"Basic salary is="<<bs<<endl;
    cout<<"HRA is="<<hra<<endl;
```