
# ▶ The Dangling Else Problem

f_discount = 0.30;
}
else
{
if(c_gender == 'F')
f_discount = 0.05;
}
f_payment = f_premium - (f_premium * f_discount);
printf("Amount to be paid after discount of %0.2f(%)",f_discount*100);
printf(" is %0.2f\n", f_payment);

return;
}
/* End of main function */

# Output 1:

Enter premium: 15000

Had accident last year y/y for yes: n

Enter gender F/f for Female: f

Amount to be paid after discount of 35.00(%) is 9750.00

# Output 2:

Enter premium: 15000

Had accident last year y/y for yes: n

Enter gender F/f for Female: m

Amount to be paid after discount of 30.00(%) is 10500.00

# Output 3:

Enter premium: 15000

Had accident last year y/y for yes: y

Enter gender F/f for Female: m

Amount to be paid after discount of 0.00(%) is 15000.00

# Output 4:

Enter premium : 15000

Had accident last year y/y for yes: Y

Enter gender F/f for Female : F

Amount to be paid after discount of 5.00(%) is 14250.00

It can be seen in Program 6 that we have included an additional file ctype.h. This file is required for the successful operation of inbuilt function toupper used in the program. The function toupper converts the character entered from keyboard to an upper case character, so that the handling of the if statement becomes easier. Observe that we have used the if-else statement in the true action block of condition if(c_accident != 'Y'), while the if statement has been used in the false action block.

When the if statements are nested to more than one level, it leads to a dangling else problem. The next section discusses the dangling else problem.

# ▶ The Dangling Else Problem

The C compiler allows us to use the if statement in various combinations. One such combination is nesting of the if statements. When the if statements are nested, at times a problem of dangling else is encountered by the compiler. The term dangling else indicates that the C compiler is not able to locate a pair of if-else properly. To resolve the problem of dangling else, the compiler associates the else statement with the immediate preceding if statement. Thus, the output of the code may then not be as per the need of the user. Program 7 illustrates the dangling else problem:

# ▶ Program 7

```c
/* Program to illustrate the dangling else problem */
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
    scanf("%f", &f_premium);

    c_temp = getchar();

    printf("\nHad accident last year Y/y for yes: ");
    scanf("%c", &c_accident);
    c_accident = toupper(c_accident);

    c_temp = getchar();

    printf("\nEnter gender F/f for Female : ");
    scanf("%c", &c_gender);
    c_gender = toupper(c_gender);

    c_temp = getchar();
    /* Calculate premium */

    if(c_accident != 'Y')
    if(c_gender == 'F')
    f_discount = 0.35;
    else
    if(c_gender == 'F')
    f_discount = 0.05;

    f_payment = f_premium - (f_premium * f_discount);
    printf("Amount to be paid after discount of %0.2f(%)", f_discount*100);
    printf(" is %0.2f\n", f_payment);
    return;
}
/* End of main function */
```

# Output 1:

Enter premium: 25000
Had accident last year Y/y for yes: Y
Enter gender F/f for Female: F
Amount to be paid after discount of 0.00(%) is 25000.00

# Output 2:

Enter premium: 15000
Had accident last year Y/y for yes: N
Enter gender F/f for Female: F
Amount to be paid after discount of 35.00(%) is 9750.00

Program 7 was designed to calculate the premium to be paid to an insurance company based on certain criteria. Figure 6 shows the problem of dangling else problem and its solution.

![](img/5d422ba7108ffdf64376be51eaf0c459_130_0.png)

▲ Figure 6: Dangling Else Statement

It can be observed in Figure 6 that the use of scope removes the problem of dangling else. In most cases, the user has to be careful and avoid dangling else by using proper scope of statements.

For small set of available alternatives, the two-way selections work fine. As the number of alternatives increases, the use of two-way selection becomes complex. If we have more number of alternatives, then we have to go for multiway selection. The next subsection discusses how multiway selection is implemented in C.

# ■ **The Multiway Selection**

At times we need to make a multiway selection based on several conditions. C supports two decision structures, namely, if-else ladder and switch, which allow multiway selection. The if-else ladder is a variant of the if-else statement studied earlier, while switch has its own structure. The next subsection discusses how to use the if-else ladder.

# ■ **The If-Else Ladder Statement**

The if-else ladder is more commonly known as else-if ladder as it associates the else statement with another if. The ladder is formed by cascading several conditions else part with if statement. The conditions are evaluated from top to bottom in the ladder. As soon as one of the test conditions is evaluated to true, its corresponding action block is executed. Once the execution of the true action block is over, the execution of the entire if statement stops. The syntax of the else if ladder is as follows:

```text
if( test condition 1 )
    action statement 1;
else if( test condition 2 )
    action statement 2;
:
:
else if (test condition n)
    action statement n;
else
    default action statement;
```

It can be observed in the preceding syntax that we start with the if-else statement, then with every else statement we have appended the if statement. The last else statement becomes a default action statement. In case all the test conditions are evaluated to false, the default action statement would be executed. Figure 7 shows the logical flow of the else-if ladder:

![](img/5d422ba7108ffdf64376be51eaf0c459_131_0.png)

It can be observed in Figure 7 that every test condition has an exit point after the execution of true action block. The worst-case scenario here would be failure of all n test conditions. In such cases, the compiler will have to check all the test conditions specified. Program 8 illustrates the use of else-if ladder:

# Program 8

```c
/*  Program to illustrate the use of if-else ladder  */
#include <stdio.h>
/*  Beginning of main function  */
main()
{
    /*  Declare variable  */
    float f_celsius;
    /*  Input data  */
    printf("Enter temperature: ");
    scanf("%f", &f_celsius);

    /*  Check the status of climate  */
    /*  Based on status print appropriate message  */
    if(f_celsius >= -40.0 && f_celsius < 10.0)
    {
        printf("It is the coldest period of year.\n");
    }
    else if(f_celsius >= 10.0 && f_celsius < 20.0)
    {
        printf("The weather is comfortable at present.\n");
    }
    else if(f_celsius >= 20.0 && f_celsius < 50.0)
    {
        printf("It is the hottest period of year.\n");
    }
    else
    {
        printf("Mankind cannot survive in this temperature.\n");
    }

    return;
}  /*  End of main function  */
```

**Output 1:**
Enter temperature: -45
Mankind cannot survive in this temperature

**Output 2:**
Enter temperature: -5
It is the coldest period of year

**Output 3:**
Enter temperature: 15.25
The weather is comfortable at present

**Output 4:**
Enter temperature: 25
It is the hottest period of year

It can be observed in Program 8 that we input a temperature in Celsius. The temperature is then compared with various ranges of values using the if-else statement. As one of the test conditions become true, the message is printed and the program stops execution.

The if-else ladder does provide us the multiway selection. However, as the number of choices increases, the complexity of the program will also increase. To make the programs look more readable and compact, C provides another multiway selection structure called switch. The next subsection discusses how to use a switch structure.

# The Switch Statement

The if-else structure was a derived mechanism to implement multiway selection in a C language. C provides an inbuilt decision structure called switch for multiway selection. The decision structure when used improves the readability of the program. The complete switch decision structure is made up of four C keywords, namely, switch, case, default, and break. The syntax of the switch statement is as follows:

```text
switch (expression)
{
    case value 1:
        [Action block 1]
        [break;]
    case value 2:
        [ Action block 2 ]
        [break;]
    case value 3:
        [ Action block 3 ]
        [break;]
    : 
    : 
    case value N:
        [Action block N]
        [break;]
    [default:
        [default action block]
        [ break ;]
    ]
}
```

It can be observed in the preceding syntax that we have used square brackets at many places. The square bracket indicates that the statements written within them are optional. The term expression immediately succeeding the switch keyword refers to an expression that can be evaluated to an integer constant or a character constant. Each case option contains an integer constant or a character constant, which is known as case label. The case labels always end with a colon (:).

The expression value once evaluated is compared with the values specified along with the case keyword from top to bottom. When the expression value matches with the case value, the compiler starts to execute the statements mentioned in this case of switch structure. To come out of a particular block of case within the switch structure, we use
