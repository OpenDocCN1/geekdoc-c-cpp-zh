# The if Statement

If expression evaluates to true, statement1 is executed. If expression evaluates to false, control goes to the else statement, statement2, which is then executed. Both statement1 and statement2 are compound statements or blocks.

Listing 4.4 shows the program in Listing 4.3 rewritten to use an if statement with an else clause.

# Input ▼

**LISTING 4.4 agechecker2.c: An if Statement with an else Clause**

```
1: // Demonstrates if and else statements and some of C's relational operators
2:
3: #define CURRENTYEAR 2013
4: #include <stdio.h>
5:
6:     int birth_year, age;
7:
8:     int main(void)
9:     {
10:        printf("Enter the year you were born: %*");
11:        scanf("%d", &birth_year);
12:
13:        // Two tests to calculate whether the user was a leap year birth
14:
15:        if (birth_year % 4 == 0)
16:            printf("You were born in a leap year!\n");
17:        else
18:            printf("You were not born in a leap year!\n");
19:
20:        age = CURRENTYEAR - birth_year;
21:
22:        // Can check on voting age as well as drinking age
23:
24:        if (age >= 18)
25:            printf("You can vote this year!\n");
26:        if (age <= 21)
27:            printf("It is illegal for you to drink alcohol!\n");
28:
29:
30:        return(0);
31:    }
```

# Output ▼

Enter the year you were born: 1975
You were not born in a leap year!
You can vote this year!