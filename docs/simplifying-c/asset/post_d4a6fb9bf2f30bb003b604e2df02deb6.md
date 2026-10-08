
Enter value of the second variable: 293484638.82765291
Second = 293484638.827653

Enter value of the third variable: 3847596212.9876539942
Third = 3847596212.987654

The output of Program 2 shows that the input values that are specified and the output values obtained differed. The floating point numbers when used leads to loss of precision. This is very evident from the output obtained. The input and output values of the identifier first match up to first seven digits, while in case of the identifiers second and third, the input and output values match up to first 16 digits. These matching digits are considered as precision digits. To get better accuracy of results in a program, it is advisable to use higher precision. Using float values, we get broader range on values as compared to integer.

## Character

The data that is given to a program does not only consists numbers, but also includes alphabet or special characters. Such values cannot be stored by using the data type int or float. To store such values, we have to use a keyword char. The data type char utilizes 1 byte of memory storage space. In C language, a character, whether printable or nonprintable, is associated with an integer value called the American Standard Code for Information Interchange (ASCII) value. We can add a modifier unsigned to char data type also. Table 5 gives a brief description of the character data type:

**Table 5: Character Data Type**

| Data Type | Memory Allocated by the Compiler in Bytes | Description | Value Range in ASCII |
| :--- | :--- | :--- | :--- |
| char | 1 | To store a printable or nonprintable character | − 128 to + 127 |
| unsigned char | 1 | | 0 to 255 |

Program 3 shows the usage of char data type. The program written here simply accepts a character and displays the character as well as its ASCII values on the monitor screen.

### Program 3

```c
/* Program to illustrate the use of character data type*/
#include <stdio.h>

/* Beginning of main function */
main( )
{
    /* Declare a character variable */
    char c_choice;

    /* Print the character and its ASCII value */
    printf("\n Enter your choice : ");
    scanf("%c",&c_choice);

    printf("\n Choice = %c\n", c_choice);
    printf("\n ASCII value of choice = %d\n",c_choice);
    return;
}
/* End of function main */
```

Output 1:
```
Enter your choice: r
Choice = r

ASCII value of choice = 114
```

Output 2:
```
Enter your choice: R
Choice = R

ASCII value of choice = 82
```

Output 3:
```
Enter your choice:
Choice = 

ASCII value of choice = 32
```

Output 4:
```
Enter your choice: 2
Choice = 2

ASCII value of choice = 50
```

Output 5:
```
Enter your choice: $
Choice = $

ASCII value of choice = 36
```

Five different outputs of Program 3 are given here. The characters in Outputs 1 and 2 are both alphabet r; however, one is in lower case, while the other is in upper case. Due to the change in case, the ASCII values of both the characters also differ. In Output 3, there does not seem to be any character entered; actually, at the time of giving input, the space bar was pressed. Hence, the character is not visible as an output on the screen, but still has an ASCII value. Even an Enter key is a valid input for a character data type identifier. A user has to be a little bit cautious while using character data type, as at times the results could be unexpected. Output 4 is another special case where a numeric value 2 is converted to a character value 2. Finally, in Output 5, we have entered a special character.

## Empty Data Set

The last one of the primitive data types in C language is *void*. A *void* data type does not associate an identifier with a specific type, such as integer or real. It associates an identifier with an empty value. In C language, it is mainly used along with functions and pointers. As mentioned earlier, C programs consist of function. The functions used may return a value. If we don't want the function to return a value, then we prefix the function name with a void.

In all the example programs used till now, the last statement of the program is return;. This statement tells the compiler to exit from the function body. A warning message Function should return a value would appear on the screen at the time of compilation if we don't write the statement return;. To avoid getting such a message, we can prefix main( ) with void.

In the next section, we will learn about how to create a data type of our own.

## 3.3 User-Defined Data Type

C language is a flexible language; it allows the users to create new entities from the existing one. We can create a new data type by making use of the existing data type. The keyword typedef is used in C language to create a new data type. It is used to define a variable that can be used as data type in our program.

### Type Definition

The syntax for using type definition is as follows:

```c
typedef datatype identifier;
```

where datatype refers to an existing data type and the data type used can be primitive or derived. Identifier refers to new name that we want to assign to the available data type. In real sense, C language does not allow us to create a new data type. Instead, it allows us to give an alias to an existing data type. Some examples of the usage of type definition are as follows:

```c
typedef int Num;
typedef long Big;
```

The first example gives an alias Num to the integer data type, while the second example gives an alias Big to the modifier long. The new identifiers can now be used to declare an integer variable. The example of the usage of alias is as follows:

```c
Num i_roll_no;
Big i_amount;
```

Program 4 illustrates the usage of type definition:

### Program 4

```c
/* Program to illustrate the use of type definition */

#include <stdio.h>
#define PI 3.14

/* Beginning of main function */
main( )
{
    /* Give an Alias REAL to float data type */
    typedef float REAL;

    /* Declare a variable of type REAL (float) */
    REAL f_radius, f_circumference;

    /* Accept value of radius */
    printf("\n Enter the value of radius: ");
    scanf("%f",&f_radius);

    /* Calculate Circumference of Circle */
    f_circumference = 2 * PI * f_radius;
    /* Print the value of circumference */

    printf(" Circumference of Circle with radius %f is %f\n",f_radius,f_circumference);

    return;
}
/* End of function main */
```

Output:
```
Enter the value of radius : 5.5
Circumference of Circle with radius 5.5 is 34.540001
```

In Program 4, observe the first executable statement after main( ). where the data type float has been given an alias REAL. The alias has been written in upper case just to separate it from normal identifiers. The new data type has then been used to declare two variables. The program still gives us the desired output.

The concept of aliasing a variable comes in very handy when we use derived data types in our programs. It has been used extensively in later chapters to improve the readability of the programs.

## 3.4 Derived Data Type

The primitive data types may suffice our needs in simple C programs. However, it may not be appropriate to use them if the program is complex. For example, assume that we need to store the salary of five employees. In such cases, we need to define five different variables. Handling five different variables may increase the complexity of the program itself. Similarly, if we need to store the complete information of the five employees, such as their employee number, gender, name, and salary, then we may need additional variables. Here, grouping of the variables may become a problem. To overcome these problems, C language provides us derived data types. Enumerated, Array, Pointer, Structure, and Union are examples of the derived data types available in C language. The next section discusses about the enumerated data type.

## Enumerated Data Type

Enumerated data types can be created in C language by using keyword *enum*. They allow the programmer to associate a numeric constant with predefined names. The syntax for using enum is as follows:
