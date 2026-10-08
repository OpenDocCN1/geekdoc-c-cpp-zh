
```
y = x; /* copies array x to array y */
```

## 11.2.2 Arithmetic on Structure Variables

Arithmetic operations such as addition, subtraction, multiplication, and division may be performed on appropriate members of structure variables. The arithmetic operations are performed on the members of the structure by using either the structure member operator or the structure pointer. The following example shows arithmetic operations on structure variables.

### Using the Structure Member Operator

```
struct tagname
{
    int a;
    float b;
    float c;
};
```

```
struct tagname var1, var2, var3;
var1.a = 20;
var1.b = 12.5;
var1.c = var1.a * var1.b;
var2.a = 40;
var2.b = 25.0;
var2.c = var2.a * var2.b;
```

Addition of two structures:

```
var3.a = var1.a + var2.a;
var3.b = var1.b + var2.b;
var3.c = var1.c + var2.c;
```

Notice that the addition operations are performed on the members of the structure. The addition of two structure variables is implemented using the addition of corresponding members of the structure as shown. Similarly, other arithmetic operations such as subtraction, multiplication, division, and exponentiation may be performed on structure variables using structure member operators.

### Using the Structure Pointer Dereference Operator

``` evenstruct tagname
{
    int a;
    float b;
    float c;
};
```

```
struct tagname var1, var2, var3, *ptr1, *ptr2, *ptr3;
ptr1 = &var1;
ptr2 = &var2;
ptr3 = &var3;

ptr1 -> a = 20;
ptr1 -> b = 12.5;
ptr1 -> c = ptr1 ->a * ptr1 ->b;

ptr2 -> a = 40;
ptr2 -> b = 25.0;
ptr2 -> c = ptr2 -> a * ptr2 -> b;
```

Addition of two structures:

```
ptr3 -> a = ptr1 -> a + ptr2 -> a;
ptr3 -> b = ptr1 -> b + ptr2 -> b;
ptr3 -> c = ptr1 -> c + ptr2 -> c;
```

Notice that the dereference operator is used to access the members of the structure using the structure variable pointer. Similarly, other arithmetic operations may be performed on structure variables.

## 11.2.3 The typedef Statement and its Usage

The typedef statement lets the programmer provide a synonym for either user-defined or the base data types. The typedef is used when the structure is declared or after the structure is declared. The following code shows the declaration of structure variables by use of the typedef construct.

```c
typedef struct record
{
    char name[20];
    int hours;
    float hourly_rate;
    float gross;
    float net;
} RECORD;
```

or

```c
struct record
{
    char name[20];
    int hours;
    float hourly_rate;
    float gross;
    float net;
};
```

```c
typedef struct record RECORD;
```

Both forms are valid and RECORD is the synonym for record, the structure tag of the structure.

The structure variables may be declared using the typedef name RECORD as follows:

```c
RECORD record1, record2, record[5];
```

The structure variables are record1, record2, and a structure variable array with five elements is record[5]. The short name RECORD is used to define the structure variables instead of struct record. This is a compact form to provide a data type name for the structure. It is required in order to pass structures to functions and return them. This use of typedef is shown in the next section.

## 11.2.4 Review Questions

- 1. Indicate whether the following statements are true or false.
    a. Input into a structure variable is effectively input into the individual members of the structure.
    b. Data input and output may be done using either the structure member operator or by using a pointer dereference operator.
    c. The assignment of values to structure variables is accomplished by using the structure member operator or a structure pointer dereference operator.
    d. A structure variable may be assigned to another structure variable provided both structure variables have the same structure data type.

- 2. Write an input statement to input data to the members of the structure variable colm1.

```c
struct sticolumn      /* steel column data */
{
    int numcolumns;
    float diameter;
    float length;
};

struct sticolumn colm1;
```

- 3. Write an output statement to output the data members of the structure variable colm1.

```c
struct st1column {
    int nuncolumns;
    float diameter;
    float length;
};

struct st1column colm1;
```

- 4. Write a typedef statement for the following structure and declare two single variables and the one-dimensional array using the typedef name.

```c
struct strength {
    float load;
    float diameter;
    float length;
    float stress;
    float strain;
};
```

Declare a structure type vector to hold any size vector of up to 10 elements, where the number of elements is part of the structure.

## 11.3 Structures and Functions

A structure variable may be passed to a function in the same way a scalar variable of a basic data type is passed, by value or by pointer. A function can return a variable structure data type. If a function is returning a structure variable, the return data type in the function prototype and in the function header must be a structure data type. When structure variables are passed to a function as arguments, the parameters in the function prototype and in the function header must be of the same structure data type. In the function prototype the variable names for the parameters are optional, but in the function header of the function definition, variable names must be specified for the function parameters. When structures are passed between functions, the typedef statement must be used. The following sections show the passing of structures to functions by value and by pointer.

### 11.3.1 Passing Structure Variables by Value

Structure variables are passed by value simply by naming the variables in the function call.

For example, consider the following structure:

```c
#include <stdio.h>

struct cylinder {
    float radius;
    float length;
    float section;
    float volume;
};
typedef struct cylinder CYLINDER;

void funcoutput(CYLINDER);
int main() {
    CYLINDER can;
    const float PI = 3.141593;
    scanf("%f %f %f", &can.radius, &can.length, &can.section);
    can.section = PI * can.radius * can.radius;
    can.volume = can.length * can.section;
    funcoutput(can);
    return 0;
}

void funcoutput(CYLINDER) {
    printf("Radius: %f\n", can.radius);
    printf("Length: %f\n", can.length);
    printf("Section: %f\n", can.section);
    printf("Volume: %f\n", can.volume);
    return;
}
```

Notice that the function passes the CYLINDER variable to the function by value. In C, variables of all named data types are passed by value or by pointer. The function funcoutput receives the structure by value and the structure variable can in the function header is used to access the members of a copy of the CYLINDER variable defined in the main function.

The following sample program shows the passing of several structure variables by value. This program computes the stress and strain in a steel column subject to compression load in pounds. The modulus of elasticity for steel is given as E = 30 × 10⁶ psi.

```c
#include <stdio.h>

struct column
{
    float diameter;
    float compload;
    float stress;
    float strain;
};
typedef struct column COLUMN;

float fnstress(COLUMN);
double fnstrain(COLUMN);
void foutput(COLUMN)
int main()
{
    struct column steelcol;
    scanf("%f %f", &steelcol.diameter,&steelcol.compload);
    steelcol.stress = fnstress(steelcol);
    steelcol.strain = fnstrain(steelcol);
    foutput(steelcol);
    return 0;
}
```

```c
float fnstress(COLUMN steelcolumn1)
{
    const float PI = 3.141593;
    float area, tempstress;
    area = (PI * steelcolumn1.diameter * steelcolumn1.diameter)/4.0;
    tempstress = steelcolumn1.compload / area;
    return tempstress;
}
```

```c
double fnstrain(COLUMN steelcolm1)
{
    const float E = 30000000.00;
    double tempstrain;
    tempstrain = steelcolm1.stress / E;
    return tempstrain;
}
```
