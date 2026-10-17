
things would turn out to be pretty tedious especially when you realize that apart from these details you also want to store particulars like his address, the telephone number, license number and so on.

These things can get tedious even with arrays because that many arrays have to be declared and apart from those a battery of for loops have to be declared and the program would go haywire and the number of lines would shoot up beyond expectations and lastly just imagine the error finding process. You would probably spend the rest of your programming life searching for an error. Whew! This is where structures does the superman act.

By declaring the three variables in a structure these variables can be accessed any number of times by just using the subscript of the structure. The Pointer, Arrays, and other Structures can also be inducted as elements within a defined structure. The individual structure elements that is the int, char declared inside a structure are referred to as members of that particular structure. The structure once declared can be accessed and processed within a program.

Apart from this, the structures also spread its tentacles to other aspects of C and are closely associated with the functions, arrays, and pointers. More details will be splashed out in the later parts of this session and you will appreciate the structures once you have a detailed outlook at all those concepts.

## 8.3. DECLARING AND ACCESSING A STRUCTURE

After having an insight about the advantages and the definition of structure you shall now learn how to declare a structure. As talked of earlier that structure is a data type and like the rest of the data types it is also a keyword and it is written as “struct.” This has to be allotted a name referred to as “tag” or simply structure name and below it the different members are mentioned.

These members are nothing but variables with their data types mentioned. The general format is described below:

```c
struct tag
{
    datatype variable name;
    datatype variable name;
};
```

An example is given below:

```c
struct employee
{
    int eno;
    char ename;
    float esal;
};
```

From the above, e.g., you can see that the keyword struct is mandatory followed by the structure name and it opens braces for the members. The structure members here are the eno, ename, and esal and each of them are terminated with a semicolon and the closing braces for the structure is also terminated with a semicolon.

### Initializing the members

Once the new structure data type has been declared, variables as per the programmer's request can be defined of that type. For example, the structure variables e1, e2, e3 can be declared of the data type struct employee as depicted below:

```c
struct employee e1, e2, e3;
```

Now the question arises: where do you declare the above statement? This can be done in the following different ways after the closing braces of the structures.

```c
};
/* closing brace */

struct employee e1, e2, e3;
```
OR
```c
} e1, e2, e3;
```

Once the declaring has been done you need to know if initializing can be done while declaring and the answer is positive. The format must be familiar to you, as it is similar to the one used in arrays. Take a look below at the format:

```c
struct employee
{
    char ename[10];
    float esal;
    int eno;
};

struct employee e1 = {"Johnny", 500.00, 101};
struct employee e2 = {"Davis", 1000.00, 102};
```

If you are not happy with this type of initializing the other type is to request the user with the help of the scanf(). This type will be dealt with later.

### Accessing members

Now that you have declared and initialized the structure variable it's time to check out how to access the variables so that they can be used in the program (Figure 8.1).

![](img/c948b22e3869eae71cd653f0917e0009_137_0.png)

**Figure 8.1.** Declaring and accessing a structure.

You used a subscript for accessing elements in the array. Here you use a dot (.) to access the data. Say you want the salary of the second employee, then it can be written in the following way. `e2.esal`. The e2 is called the structure variable and esal the element.

A dot must exist between the structure variable and the structure member.

## 8.4. INTERNAL REPRESENTATION OF THE STRUCTURE

Since so much goes on while declaring, initializing, and accessing a structure, where do all the variables and values actually get stored in the memory? All elements of a structure regardless of the number or type are stored in contiguous memory locations and the number of bytes assigned to the data types are the same as before. The internal representation of the details of the first employee, “Johnny” with a salary of 500.00, employee ID of 101, and a few additional numerical values, stored in contiguous memory locations might look like this:

Memory Layout:

| Variable | Value | Memory-Address |
|---|---|---|
| E | 'E' | 0x1000 |
| Name | "Johnny" | 0x1001 |
| Salary | 500.00 | 0x1008 |
| Employee ID | 101 | 0x100C |
| Additional | 1111 | 0x1010 |
| Additional | 1112 | 0x1014 |
| Additional | 1116 | 0x1018 |

A simple program using structure:

```c
/* program that accepts values and displays it back */
#include<stdio.h>
void main()
{
    struct emp
    {
        char ename[15];
        float esal;
        int eno;
    };
    struct emp e1, e2, e3;
    printf("Enter name,salaries and identity number of employees\n");
    scanf(" %s %f %d", &e1.ename, &e1.esal, &e1.eno);
    scanf(" %s %f %d", &e2.ename, &e2.esal, &e2.eno);
    scanf(" %s %f %d", &e3.ename, &e3.esal, &e3.eno);
    printf("You have entered the following data:");
    printf(" %s %f %d", e1.ename, e1.esal, e1.eno);
    printf(" %s %f %d", e2.ename, e2.esal, e2.eno);
    printf(" %s %f %d", e3.ename, e3.esal, e3.eno);
}
```

In the above program you can see that the structure members are declared inside the structure and the structure variables, i.e., e1, e2, e3 are declared outside the structure using the keyword struct and the structure name. The values for the structure members are requested from the user and they are accepted using the scanf.

The values are printed back by using the structure variable and the structure member with a dot (.) in between them.

## 8.5. ARRAY OF STRUCTURES

In the above program you have acclimatized yourself to the various contents in a C program using structures. The above program was perfect, since it received 3 values and displayed them back, but if the number of values was increased to 100 then you might have used 100 structure variables from b1, b2, ..., b100 but as magnanimous as C is it always provides an alternative for tedious issues.

The structures in these kind of emergencies request the arrays to act immediately. That is to say the structure variables can be declared as an array and large amount of variables can be used efficiently. To declare an array of structures the process is similar to arrays. Before the square brackets, 3 things precede it: the keyword struct, the structure name and the array name. Thus, the employee array can be declared as below.

```c
struct employee e[100];
```

You are now presented with a sample program that will cover all the aspects required to be comprehended in structures using arrays.

```c
#include<stdio.h>

struct emp
{
    char ename[15];
    int esal;
    int eno;
};

struct emp e[3];

void main()
{
    int i;
    for(i=0;i<=2;i++)
    {
        printf("\n Enter name,salary and idno");
        scanf("%s %d %d", &e[i].ename, &e[i].esal, &e[i].eno);
    }
    for(i=0;i<=2;i++)
        printf("\n %s\n%d\n%d", e[i].ename, e[i].esal, e[i].eno);
}
```

The above simple program accepts names, salaries, and id no of 15 employees and displays it back. As you can see the program accepts 15 names from the user using a for loop with the subscript variable i which has to be declared as an int. You can see that the structure has been declared externally before the main() function, so that the elements are accessible to all parts of the program. Once the array of structure is declared, i.e., by giving the statement `struct emp e[15]`, space in the memory is reserved for 15 structure types.

## 8.6. PASSING STRUCTURE INTO FUNCTIONS

Now that you have had enough knowledge about using arrays in structures it's time to knock the door of functions and try and analyze how an entire structure can be passed into a function. Before embarking on that one minor detail what you should be aware of is that individual elements of the structure also can be passed to a function but the only shortcoming in that is if there are many elements then passing those elements to a function would turn out to be a stupendous affair and it is better to refrain from such acts.

Hence the area of concern for you would be to pass an entire structure to a function. The modus operandi would be just the same and does not differ in any aspect. The one thing to be noted here is that the initialization is done at the time of declaration, i.e., in static mode.

```c
#include<stdio.h>
struct emp
{
    char ename[10];
    int eno;
    float esal;
};
void main()
{
    struct emp e1 = {"cooper", 104, 6000.00};
    pass(e1);
}
```
