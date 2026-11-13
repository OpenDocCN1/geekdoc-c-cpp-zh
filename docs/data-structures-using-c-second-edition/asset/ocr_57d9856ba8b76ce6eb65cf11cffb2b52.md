```
%d+%di",sum_c_real, sum_c_imag);
break;
case 4:
sub_c_real = c1.real - c2.real;
sub_c_imag = c1.imag - c2.imag;
printf("(%n The difference between two complex numbers
is %d+%di", sub_c_real, sub_c_imag);
break;
}while(option != 5);
getch();
return 0;
}
```

```
Output
**************** MAIN MENU *****************
1. Read the complex numbers
2. Display the complex numbers
3. Add the complex numbers
4. Subtract the complex numbers
5. EXIT
Enter your option : 1
Enter the real and imaginary parts of the first complex number : 2 3
Enter the real and imaginary parts of the second complex number : 4 5
Enter your option : 2
The first complex numbers is : 2+3i
The second complex numbers is : 4+5i
Enter your option : 3
The sum of two complex numbers is : 6+8i
Enter your option : 5
```

# 5.2 NESTED STRUCTURES

A structure can be placed within another structure, i.e., a structure may contain another structure as its member. A structure that contains another structure as its member is called a nested structure. Let us now see how we declare nested structures. Although it is possible to declare a nested structure with one declaration, it is not recommended. The easier and clearer way is to declare the structures separately and then group them in the higher level structure. When you do this, take care to check that nesting must be done from inside out (from lowest level to the most inclusive level), i.e., declare the innermost structure, then the next level structure, working towards the outer (most inclusive) structure.

```
typedef struct
{
    char first_name[20];
    char mid_name[20];
    char last_name[20];
}NAME;
typedef struct
{
    int dd;
    int mm;
    int yy;
}DATE;
typedef struct
{
    int r_no;
```