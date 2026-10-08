
It can be observed in Figure 3 that two operators, namely, relational and logical, are used in the test condition. In the first case, the result of the test condition is evaluated to true, while it is evaluated to false in the second case.

Note that although assignment operator can be used in the test condition, it will always result to a true condition. For example, a test condition (`i_number = 20`) will always evaluate to true, as the value of expression will always be 20. Many times the users use = instead of ==, and then are unable to find the error.

The simple if statement, although considered as part of the two-way selection, in real sense is a one-way selection, as the two-way selection normally have two options available. The next subsection discusses the if-else construct, which is a two-way selection.

## The If-Else statement

The if-else statement is an improvement over the simple if statement. In the simple if statement, there is only one block of action statements. This block gets executed when the test condition is evaluated to be true. In case the test condition is evaluated to be false, no action is taken. In most cases, we need an alternate option that can be executed. For example, in Program 2, we gave a discount of 15% only when the purchase amount was greater than equals to Rs. 5000 and the customer was a regular customer. Assume that we want to give discount to nonregular customers also. In such case, we need two alternatives: one that gives discount to regular customers and the other that gives discount to nonregular customers. This can be easily achieved by making use of the if-else statement.

The syntax of the if-else statement is as follows:

```
if( test condition )
{
    True action statements;
}
else
{
    False action statements;
}
```

It can be observed in the preceding syntax that the if-else statement has two action statement blocks. If the test condition is evaluated to be true, the true action statements block is executed. In case the test condition is evaluated to be false, the false action statements block is executed. In all cases, either of the two action blocks will always be executed. Figure 4 illustrates the logical flow of the if-else statement:

![](img/5d422ba7108ffdf64376be51eaf0c459_123_0.png)

▲ Figure 4: Logical Flow of the If-Else Statement

It can be observed that Figure 4 is exactly the same as Figure 1. Here, we can see two mutually different flow paths: one for true case and another for false case. Regardless of the case chosen, after execution of either of the blocks, the control flow is transferred to the next statement in sequence. Program 3 illustrates the use of if-else statement:

## Program 3

```
/* Program to illustrate the use of if-else statement */
#include<stdio.h>
/* Beginning of main function */
main()
{
/* Declare variables */
float f_purchase, f_discount = 0.0;
float f_dis_amount, f_payment;
char c_regular, c_temp;
/* Read values */
printf("\nEnter total purchase amount: ");
scanf("%f",&f_purchase);
c_temp = getchar();
printf("\nEnter Y or y if regular customer: ");
scanf("%c",&c_regular);
if (f_purchase >= 5000.00 && (c_regular == 'Y' || c_regular == 'y'))
f_discount = 0.15;
else
f_discount = 0.10;
/* Calculate discount amount */
f_dis_amount = f_purchase * f_discount;

/* Calculate Payment */
f_payment = f_purchase - f_dis_amount;

/* Output Data */
printf("\nTotal payment to be made Rs. %0.2f\n", f_payment);
printf("Total discount availed Rs. %0.2f\n", f_dis_amount);

return;
}

/* End of main function */
```

**Output 1:**

```
Enter total purchase amount: 5000
Enter Y or y if regular customer: y

Total payment to be made Rs. 4250.00
Total discount availed Rs. 750.00
```

**Output 2:**

```
Enter total purchase amount: 6000
Enter Y or y if regular customer: n
Total payment to be made Rs. 5400.00
Total discount availed Rs. 600.00
```

**Output 3:**

```
Enter total purchase amount: 4500
Enter Y or y if regular customer: y

Total payment to be made Rs. 4050.00
Total discount availed Rs. 450.00
```

It can be observed in Program 3 that only in the case when the purchase value is greater than or equal to Rs. 5000 and the customer is regular, a discount of 15% is given. In all other cases, the discount is 10%. It does not matter whether the customer is regular or not or if the purchase made is less than Rs. 5000. The outputs 2 and 3 show the result of such cases. Let us take one more example, that is, Program 4, to understand the if-else statement better.

## Program 4

```
/* Program to illustrate the use of if-else statement */

#include <stdio.h>

/* Beginning of main function */
main()
{
   /* Declare variable */
   char c_char;
   /* Input Data */
   printf("Enter an alphabet : ");
   scanf("%c",&c_char);

   /* Check if the alphabet is upper case */
   if (c_char >= 65 && c_char <=90)
   {
       printf("The alphabet entered is upper case\n");
       c_char += 32;
       printf("The alphabet in lower case is %c\n",c_char);
   }
   else
   {
       printf("The '%c' is not an upper case alphabet.\n",c_char);
   }
   return;
} /* End of main function */
```

**Output 1:**

```
Enter an alphabet : H
The alphabet entered is upper case
The alphabet in lower case is h
```

**Output 2:**

```
Enter an alphabet : *
The '*' is not an upper case alphabet
```

**Output 3:**

```
Enter an alphabet : h
The 'h' is not an upper case alphabet
```

It can be observed in Program 4 that in case the test condition is evaluated to true, three statements get executed. The first statement prints the message The alphabet entered is upper case, the second statement adds an American Standard Code for Information Interchange (ASCII) value 32 in the ASCII value of the character read, and the third statement prints the lower case character.

Many times we need to combine the if statement and the if-else statement to get a desired result. This formation gives rise to another if statement format called nested if statement. The next subsection discusses the nested if statement.

## The Nested If Statement

It has been already mentioned that when if statement is used within another if statement, it is called nested if statement. The order of appearance of the if statement is not significant. The if statement may appear either in true action statement block, or in false action statement block, or in both. Figure 5 illustrates the logical flow of nested if statement:

![](img/5d422ba7108ffdf64376be51eaf0c459_126_0.png)

▲ Figure 5: Logical Flow of the Nested If Statement

It can be observed in Figure 5 that we have used three if-else statements. The flow of the figure indicates that, in any case, minimum two if-else statements would be executed. It is not necessary that both the true and false action blocks should always contain if statement. Program 5 illustrates the use of nested if statements:

## Program 5

```
/* Program to illustrate the use of nested if statement */
#include <stdio.h>
/* Beginning of main function */
main()
{
    /* Declare variable */
    unsigned int i_year, i_rem1, i_rem2;

    /* Input Data */
    printf("Enter value for year: ");
    scanf("%u",&i_year);

    /* Calculate whether year is leap or not */
    if ((i_rem1 = i_year % 4) == 0)
    {
        i_rem2 = i_year % 100;

        if(i_rem2 == 0)
            printf("Year %u is not a leap year\n",i_year);
        else
            printf("Year %u is a leap year\n",i_year);
    }
    else
        printf("Year %u is not a leap year\n",i_year);

    return;
}
/* End of main function */
```

**Output 1:**

```
Enter value for year: 2000  
Year 2000 is not a leap year
```

**Output 2:**

```
Enter value for year: 2010  
Year 2010 is not a leap year
```

**Output 3:**

```
Enter value for year: 2012  
Year 2012 is a leap year
```

It can be observed in Program 5 that we have used a nested if-else statement in the true action block for the condition if ((i_rem1 = i_year % 4) == 0). In case the test condition is evaluated to be false, we simply print a message that indicates that the entered year is not leap. Let us take one more example to understand the nested if statement. Program 6 illustrates how to calculate a premium after availing discount:

## Program 6

```
/* Program to illustrate the use of nested if statement */  
#include <stdio.h>  
#include <ctype.h>  
  
/* Beginning of main function */  
main()  
{  
    /* Declare variable */  
    float f_premium, f_discount=0.0, f_payment;  
    char c_gender, c_temp, c_accident;  
  
    /* Input Data */  
    printf("Enter premium: ");  
    scanf("%f",&f_premium);  
    c_temp = getchar();  
  
    printf("\nHad accident last year y/Y for yes: ");  
    scanf("%c",&c_accident);  
    c_accident = toupper(c_accident);  
  
    c_temp = getchar();  
    printf("\nEnter gender F/f for Female: ");  
    scanf("%c",&c_gender);  
    c_gender = toupper(c_gender);  
    c_temp = getchar();  
    /* Calculate premium */  
    if(c_accident != 'Y')  
    {  
        if(c_gender == 'F')  
            f_discount = 0.35;  
        else
```
