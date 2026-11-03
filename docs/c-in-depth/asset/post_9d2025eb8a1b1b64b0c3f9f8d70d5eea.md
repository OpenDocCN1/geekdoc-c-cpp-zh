
Here a new data type month is defined and the enumerator list contains six enumerators.
Internally the compiler treats these enumerators as integer constants. These are automatically assigned integer values beginning from 0, 1, 2... etc till the last member of the enumeration. In the above example these enumerators will take following values-

Jan 0
Feb 1
Mar 2
Apr 3
May 4
Jun 5

These are the default values assigned to the enumerators. It is also possible to explicitly assign value to enumerators but in this case, the successive unassigned enumerators will take values one greater than the value of the previous enumerator. For example-

```
enum month{ Jan, Feb = 4, Mar, Apr, May = 11, Jun };
```

Now the enumerators will take following values-

Jan 0
Feb 4
Mar 5
Apr 6
May 11
Jun 12

We can assign any signed integer value to enumerators, provided the value is within the range of
It is also possible to assign same value to more than one enumerator.

```
enum month{ Jan, January = 0, Feb = 1, February = 1, Mar = 2, March = 2 };
```

The enumerated variables can be processed like other integer variables. We can assign values to them from the enumerator list or they can be compared to other variables and values of the same type. For example-

```
enum month{ Jan, Feb, Mar, Apr, May, Jun } m1, m2;
m1 = Mar;
m2 = May;
```

Now m1 has integer value 2 and m2 will take the value 4.
Any variable of type enum month can take values only from the 6 enumerators specified in the enumeration.
For example this is invalid-
m1 = Dec; /*Invalid*/
Some other examples of enum data type definitions are-
enum suit{ Spades, Hearts, Clubs, Diamonds};
enum position { Ace = 1, King, Queen, Jack, Ten, Nine, Eight, Seven, Six, Five, Three, Two };
enum month{ Jan, Feb, Mar, Apr, May, Jun, Jul, Aug, Sep, Oct, Nov, Dec};
enum day{ Sunday, Monday, Tuesday, Wednesday, Thursday, Friday, Saturday};
enum color{ white, black, red, green, blue, yellow, pink, brown};

```
enum boolean{ true , false};
enum switch{ off, on};
enum subject{ Hindi, English, Maths, Physics, Chemistry, Biology, History };
enum base{ Binary = 2, Octal = 8, Decimal = 10, Hexadecimal = 16};
```

are some examples of code using these enum definitions-

```
enum color walls, floor;
if(walls==pink)
    floor=blue;
else
    floor=white;
```

```
enum day today;
today=Monday;
if(today==Sunday)
    printf("Holiday\n");
else if(today==Saturday)
    printf("Half working day\n");
else
    printf("Full working Day\n");
```

```
enum subject s;
int passmarks;
switch(s)
{
    case hindi:
    case english:
        passmarks=25;
        break;
    case maths:
        passmarks=40;
        break;
    case physics:
    case chemistry:
        passmarks=35;
        break;
    default:
        passmarks=33;
}
```

Suppose we need a function that returns number of days in a month. It can be written as-

```
enum month m;
int days;
if( m==Apr || m==Jun || m==Sep || m==Nov )
    days=30;
if( m==Jan || m==Mar || m==May || m==Jul || m==Aug || m==Oct || m==Dec)
    days=31;
if( m==Feb )
    days=28 ;
```

```
/* P14.1 Program to print the value of enum variables*/
#include<stdio.h>
main()
{
    enum month{Jan,Feb,Mar,Apr,May,Jun}m1,m2;
    m1=Mar;
    printf("m1 = %d \n",m1);
    printf("Enter value for m2 : ");
    scanf("%d",&m2);
    printf("m2 = %d \n",m2);
}
```

## Output :

m1 = 2
Enter the value for m2 : 5
m2 = 5

It is not possible to perform input and output in terms of enumerator names. The input and output only in the form of their integer values. You may be tempted to use %s to output and input enumerator variables but this is invalid since enumerators are not strings.

```
printf("%s", m1); /*Invalid*/
```

Since enumerators are identifiers so their name should be different from other identifiers in the same scope. The following code is wrong because the identifier chemistry has been used at two different places.

```
enum group1{ physics, chemistry, maths};
enum group2{ zoology, botany, chemistry }; /*Invalid*/
float maths; /* Invalid*/
```

We can use typedef in the definition of enum, for example:-

```
typedef enum{false, true} boolean;
```

Now we can define variables like this-
boolean flag = true;
We have seen earlier that we can define constants using #define also, for example:-

```
#define Sun 0
#define Mon 1
#define Tue 2
#define Wed 3
```

Now we'll compare the constants defined by #define preprocessor directive and enum.

- (i) By defining an enum, we define a new type whose variables can be declared but using #define we can only give name to some constant values.
- (ii) enum is a part of C language (32 keywords) but #define is not.
- (iii) All #define directives are global, while enum obeys the scope rules.
- (iv) In #define we have to explicitly assign the values to all constants, while in enum the value assigned by the compiler automatically.

We can always write our programs by using integer variables instead of enumerated variables, but use of enum in complicated programs makes the program more understandable.

## 14.2 Storage Classes

In addition to data type, each variable has one more attribute known as storage class. The proper use of storage classes makes our program efficient and fast. In larger multifile programs the knowledge of storage classes is indispensable. We can specify a storage class while declaring a variable. The general syntax is-
storage_class datatype variable_name;

- There are four types of storage classes-
- 1. Automatic
- 2. External
- 3. Static
- 4. Register

The keywords auto, static, register, extern are used for these storage classes. So we may write declaration statements like this-
auto int x, y;
static float d;
register int z;

When the storage class specifier is not present in the declaration, compiler assumes a default storage class based on the place of declaration.

A storage class decides about these four aspects of a variable-

- (1) Lifetime - Time between the creation and destruction of a variable.
- (2) Scope - Locations where the variable is available for use.
- (3) Initial value - Default value taken by an uninitialized variable.
- (4) Place of storage - Place in memory where the storage is allocated for the variable.

Now we'll discuss all these storage classes one by one in detail.

### 14.2.1 Automatic

All the variables declared inside a block/function without any storage class specifier are called automatic variables. We may also use the keyword auto to declare automatic variables, although this is generally not done. The following two declaration statements are equivalent and both declare a and b to be automatic variables of type int.

```
func()
{
    int a,b;
    ....
}
```

```
func()
{
    auto int a,b;
    .......
}
```

The uninitialized automatic variables initially contain garbage value. The scope of these variables is inside the function or block in which they are declared and they can't be used in any other function/block.

In the next program, there are different blocks inside main(), and the variable x declared in different blocks is different.

```
*P14.4 Program to understand automatic variables*
#include<stdio.h>
main()
int x=3;
printf("%d\t",x);
{
int x=10;
printf("%d\t",x);
}
{
int x=26;
printf("%d\t",x);
}
printf("%d\n",x);
```

Output:

3 10 26 3

### 14.2.2 External

The variables that have to be used by many functions and different files can be declared as external variables. The initial value of an uninitialized external variable is zero.

Before studying external variables, let us first understand the difference between their definition and declaration. The declaration of an external variable declares the type and name of the variable, while the definition reserves storage for the variable as well as behaves as a declaration. The keyword extern is specified in declaration but not in definition. For example the definition of an external variable salary will be written as-
float salary;
Its declaration will be written as-
extern float salary;

The following points will clarify the concept of definition and declaration of an external variable.

- Definition of an external variable-
- (a) Definition creates the variable, so memory is allocated at the time of definition.
- (b) There can be only one definition.
- (c) The variable can be initialized with the definition and initializer should be constant.
- (d) The keyword extern is not specified in the definition. Some compilers may allow the use of extern but it is better to omit this keyword in the definition.
- (e) The definition can be written only outside functions.
- Declaration of an external variable-
- (a) The declaration does not create the variable, it only refers to a variable that has already been created somewhere, so memory is not allocated at the time of declaration.
