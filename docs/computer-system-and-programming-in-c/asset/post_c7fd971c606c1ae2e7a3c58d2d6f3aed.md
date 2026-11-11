
Here salary symbolizes int and average symbolizes float. They can be later used to declare variables as follows:

salary dept1, dept2;
average section1, section2;

Therefore, dept1 and dept2 are indirectly declared as integer datatype and section1 and section2 are indirectly float data type.

```c
enum identifier {
  saturday,
  sunday = 0,
  monday,
  tuesday,
  wednesday,
  thursday,
  friday
} workday;
```

## ENUMERATED TYPE DECLARATION

An enumeration consists of a set of named integer constants. An enumeration type declaration gives the name of the (optional) enumeration tag and defines the set of named integer identifiers (called the “enumeration set”/“enumerator constants,” “enumerators,” or “members”). A variable with enumeration type stores one of the values of the enumeration set defined by that type.

Variables of enum type can be used in indexing expressions and as operands of all arithmetic and relational operators. Enumerations provide an alternative to the #define preprocessor directive with the advantages that the values can be generated for you and obey normal scoping rules.

In ANSI C, the expressions that define the value of an enumerator constant always have int type; thus, the storage associated with an enumeration variable is the storage required for a single int value. An enumeration constant or a value of enumerated type can be used anywhere the C language permits an integer expression.

The general syntax for defining an enumerated data type is as follows:

enum identifier {value1, value2 .... value n};

The identifier is a user defined enumerated data type which can be used to declare variables that have one of the values enclosed within the braces. After the definition we can declare variables to be of this 'new' type as below.

enum identifier V1, V2, V3, ........ Vn

The enumerated variables V1, V2, ........ Vn can have only one of the values value1, value2 ..... value n

### Example

```c
enum DAY /* Defines an enumeration type */
```

The value 0 is associated with Saturday by default. The identifier Sunday is explicitly set to 0. The remaining identifiers are given the values 1 through 5 by default.

## STORAGE CLASSES

The variables can be characterized by their data type and by their storage class. One way to classify a variable is according to its data type and the other can be through its storage class. Data type refers to the type of value represented by a variable whereas storage class refers to the permanence of a variable and its scope within the program, i.e. portion of the program over which variable is recognized.

The storage class associated with a variable can sometimes be established by the location of the variable declaration within the program or by prefixing keywords to variables declarations.

Moreover, a variable’s storage class tells us:

- Where the variable would be stored.
- What will be the initial value of the variable, if initial value is not specifically assigned (i.e. the default initial value).
- What is the scope of the variable, i.e. in which functions the value of the variable would be available.
- What is the life of the variable, i.e. how long would the variable exist.

C programming language consists of four storage classes which are as follows:

- (a) Automatic storage class
- (b) Register storage class
- (c) Static storage class
- (d) External storage class

Now we will discuss these storage classes one by one.

### Automatic Storage Class

The following are the key points for the automatic storage class

- They are declared at the start of a program’s block such as in the curly braces ({ }). Memory is allocated automatically upon entry to a block and freed automatically upon exit from the block.
- The scope of automatic variables is local to the block in which they are declared, including any blocks nested within that block. For these reasons, they are also called **local variables**.
- No block outside the defining block may have direct access to automatic variables (by variable name), but they may be accessed indirectly by other blocks and/or functions using pointers.
- Automatic variables may be specified upon declaration to be of storage class auto. However, it is not required to use the keyword auto because by default, storage class within a block is auto.
- Automatic variables declared with initializers are initialized every time the block in which they are declared is entered or accessed.

The features of a variable defined to have an automatic storage class are as follows:

|  |  |
| --- | --- |
| Storage | Memory |
| Default initial value | An unpredictable value, which is often called a garbage value |
| Scope | Local to the block in which the variable is defined |
| Life | Till the control remains within the block in which the variable is defined |

The following program shows how an automatic storage class variable is declared, and the fact that if the variable is not initialized it contains a garbage value.

```c
void main( )
{
auto int i, j;
printf ( "\n%d %d", i, j );
}
```

The output of the above program could be...

1223 1224

Here, 1223 and 1224 are garbage values of i and j. When you run this program you may get different values, since garbage values are unpredictable. So always make it a point that you initialize the automatic variables properly, otherwise you are likely to get unexpected results. Note that the keyword for this storage class is **auto**, and not automatic.

Scope and life of an automatic variable is illustrated in the following program.

```c
void main( )
{
    auto int i = 2;
    {
        printf ( "\n%d", i );
    }
    printf ( "%d", i );
}
```

The output of the above program is:

2 2 2

This is because, all **printf ( )** statements occur within the outermost block (a block is all statements enclosed within a pair of braces) in which i has been defined. It means the scope of i is local to the block in which it is defined. The moment the control comes out of the block in which the variable is defined, the variable and its value is irretrievably lost.

To understand this go through the following program segment

```c
void main ( )
{
    auto int i = 4;
    {
        auto int i = 5;
        {
            auto int i = 6;
            printf ( "\n%d", i );
        }
        printf ( "%d", i );
    }
    printf ( "%d", i );
}
```

The output of the above program would be:

6 5 4

The explanation of the above code is as follows:

Note that the compiler treats the three i's as totally different variables, since they are defined in different blocks. Once the control comes out of the innermost block the variable i with value 6 is lost, and hence i in the second `printf()` refers to i with value 5. Similarly, when the control comes out of the next innermost block, the third `printf()` refers to the i with value 4.

### Register Storage Class

The following are the key points for the register storage class:

- Automatic variables are allocated storage in the main memory of the computer; however, for most computers, accessing data in memory is considerably slower than processing directly in the CPU.
- Registers are memory located within the CPU itself where data can be stored and accessed quickly. Normally, the compiler determines what data is to be stored in the registers of the CPU at what times.
- However, the C language provides the storage class register so that the programmer can suggest to the compiler that particular automatic variables should be allocated to CPU registers, if possible and it is not an obligation for the CPU to do this.
- Thus, register variables provide a certain control over efficiency of program execution.
- Variables which are used repeatedly or whose access times are critical may be declared to be of storage class register.
- Variables can be declared as a register as follows:

```c
register int var;
```

The features of a variable defined to be of register storage class are as follows:

|  |  |
| --- | --- |
| Storage | CPU registers |
| Default initial value | Garbage value |
| Scope | Local to the block in which the variable is defined |
| Life | Till the control remains within the block in which the variable is defined |

A value stored in a CPU register can always be accessed faster than the one that is stored in memory. Therefore, if a variable is used at many places in a program it is better to declare its storage class as register. A good example of frequently used variables is loop counters. We can name their storage class as register.

### Example

```c
void main()
{
register int i ;
for (i = 1; i <= 100 ; i++)
printf("%d", i);
}
```

Here, even though we have declared the storage class of i as register, we cannot say for sure that the value of i would be stored in a CPU register. Why? Because the number of CPU registers are limited, and they may be busy doing some other task. What happens in such an event... the variable works as if its storage class is auto. Not every type of variable can be stored in a CPU register.

For example, if the microprocessor has 16-bit registers then they cannot hold a float value or a double value, which require 4 and 8 bytes respectively. However, if you use the register storage class for a float or a double variable you will not get any error messages. All that would happen is the compiler would treat the variables to be of auto storage class.

### External Storage Class

The following are the key points for the external storage class:

- All variables we have seen so far have had limited scope (the block in which they are declared) and limited lifetimes (as for automatic variables).
- However, in some applications it may be useful to have data which is accessible from within any block and/or which remains in existence for the entire execution of the program. Such variables are called global variables, and the C language provides storage classes which can meet these requirements; namely, the `external` (extern) and `static` (static) classes.
