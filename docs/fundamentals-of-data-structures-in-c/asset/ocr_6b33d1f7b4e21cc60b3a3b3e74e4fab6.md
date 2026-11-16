| Data type | Size (bytes) | Range |
| :--- | :--- | :--- |
| char or signed char | 1 | -128 to 127 |
| unsigned char | 1 | 0 to 255 |
| int | 2 | -32768 to 32767 |
| short int or signed short int | 2 | -32,768 to 32,767 |
| int or signed int | 2 | -32,768 to 32,767 |
| unsigned short int | 2 | 0 to 65,535 |
| unsigned int | 2 | 0 to 65535 |
| long int or signed long int | 4 | -2,147,483,648 to 2,147,483,647 |
| unsigned long int | 4 | 0 to 4,294,967,295 |
| float | 4 | 3.4e-38 to 3.4e+38 |
| double | 8 | 1.7e-308 to 1.7e+308 |
| long double | 10 | 3.4e-4932 to 1.1e4932 |

# # 1.6.2 User-defined Data Types

C supports a feature known as type definition that allows the user to define new data types that are equivalent to existing data types. This technique in some situations can help to clarify the source code of a program. The user-defined data type identifier can later be used to declare variables.

# ## Type Definition

The keyword typedef is used to define new data type names. Note that you are not actually creating a new data type, but rather defining a new name for an existing data type. The general form or the syntax of defining a new data type is

```
typedef data type identifier;
```

where identifier refers to new name(s) given to the data type. Few examples of type definition are

```
typedef int age;
typedef float average;
```

where age symbolizes int and average symbolizes float. They can be later used to declare variables as

```
age child, adult;
average mark1, mark2;
```

where child and adult are declared as integer variables whereas mark1 and mark2 are declared as floating-point variables. Using type definition you can create meaningful data names for increasing the readability of the program. They also suggest the purpose of the data type names used in the program.