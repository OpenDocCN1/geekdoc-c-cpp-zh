
```text
Enter a number: 33
Enter a number: 83
Enter a number: 98
Enter a number: 78
Enter a number: 123
Enter a number: 67
Enter a number: 09
Enter a number: 56
Enter a number: 23
Enter a number: 99
The average of the array elements are 66.9
```

Let's now learn about strings.

## Strings

C++ has two types of strings - C string and the standard C++ string class. C string, as used in the C language, is a character array terminated by a NULL '\0' character. On the other hand, standard C++ includes a new class called string. This class improves on the traditional C strings in several ways. For example, we do not need to worry about creating an array of right size to hold string variables, as C++ string class handles the memory management. In addition, the string class provides the benefit of operator overloading, which gives new meanings to old operators. For example, in the string class, the + operator is overloaded so that when we write the following statement, the + operator acts as a concatenation operator:

```cpp
S1 = S2 + S3;
```

In the preceding statement, all the three are objects of string class. In C, the same thing can be done using a library function called strcat. Listing 12.3 explores some of the features of the string class:

### Listing 12.3: Showing the Features of the String Class

```cpp
1: // Demonstrating string classes in C++
2: #include <iostream>
3: #include <string>
4: using namespace std;
5:
6: int main ()
7: {
8:     string S1("Tom");                 //Initialization
9:     string S2 = "Jerry";              //Initialization
10:    string S3;
11:
12:    S3 = S1;                          //Assignment
13:    cout<< "S3 = "<<S3<<endl;
14:
15:    S3 = S1 + " and ";                //Concatenation
16:    S3 += S2;                         //Concatenation
17:    cout<< "S3 = "<<S3<<endl;
18:
19:    return 0;
20: }
```

In Listing 12.3, we have defined three objects of string class: S1, S2, and S3. At first, we have initialized S1 and S2 using two different ways. Then assignment from S1 to S3 is done at line number 12, which explains why Tom is printed by the program. The concatenation method is also executed with + and += operators and the string, Tom and Jerry, is constructed in S3. Following is the output of the preceding program:

```text
Tom
Tom and Jerry
```

Table 12.5 shows the various member functions of string class in C++:

**Table 12.5: Member Functions of the string Class**

| Member Function | Description |
|---|---|
| size | Returns the length of a string object |
| length | Returns the length of a string object |
| max_size | Returns the maximum size of a string |
| resize | Resizes a string object |
| capacity | Returns the size of allocated storage |
| reserve | Requests a change in capacity |
| clear | Clears the string |
| empty | Tests if a string is empty |
| operator [] | Gets a character in string |
| at | Gets a character in string |
| operator += | Appends a string to the end of another string |
| append | Appends a string to the end of another string |
| push_back | Appends a character to a string |
| assign | Assigns a content to a string |
| insert | Inserts a character into a string |
| erase | Erases a character from a string |
| replace | Replaces a part of a string |
| swap | Swaps the content of two strings |
| c_str | Gets a C string equivalent |
| data | Gets a string data |
| get_allocator | Gets the allocator |
| copy | Copies a sequence of characters from a string |
| find | Finds a content in a string |
| rfind | Finds the last occurrence of content in a string |
| find_first_of | Finds a character in a string |
| find_last_of | Finds a character in a string from the end |
| find_first_not_of | Finds the absence of character in a string |
| find_last_not_of | Finds the absence of character in a string from the end |
| substr | Generates a substring |
| compare | Compares two strings |
| begin | Returns an iterator to the beginning of a string |
| end | Returns an iterator to the end of a string |
| rbegin | Returns an iterator to reverse beginning |
| rend | Returns an iterator to reverse end |

Let's now learn about structures in C++.

## Structures

A structure is a collection of simple variables expressed as a single user-defined data type in C++. The variables within a structure can be of basic data types (int, char, or float) and user-defined data types (structures or enumerations). The primary reason of explaining structures in C++ basics is that the syntax of structure is almost identical to classes in C++. A structure is a collection of data; whereas, a class is a collection of data and functions. Listing 12.4 shows the use of structures in C++:

### Listing 12.4: Showing the Use of Structures in C++

```cpp
1: // Demonstrating user-defined structures in C++
2: #include <iostream>
3: using namespace std;
4:
5: struct employee_data
6: {
7:     char        employee_name[30];
8:     int         age;
9:     double      salary;
10: };
11:
12: int main ()
13: {
14:     struct employee_data emp;
15:
16:     cout<<"Enter Employee Name: ";
17:     cin >> emp.employee_name;
18:     cout<<"Enter Employee Age: ";
19:     cin >> emp.age;
20:     cout<<"Enter Employee Salary: ";
21:     cin >> emp.salary;
22:
23:     cout    <<"\nEmployee "<<emp.employee_name<<" is "
24:             <<emp.age<<" years old with Rs "<<emp.salary<<"\n";
25:
26:     return 0;
27: }
```

In Listing 12.4, line number 1 is a comment; whereas, line number 2 and line number 3 are preprocessor directives. We start declaring the structure from line number 5 to line number 10. In the program, the employee_data structure is declared with its members as employee_name, age, and salary. Note that all the declarations to a structure must end with a semicolon, as shown in line number 10. The structure declaration serves only as a blueprint for the creation of variables of type employee_data. The declaration does not itself define any variable nor does it set aside any space in the memory. It is merely a specification for how structure variables would appear when they are defined.

The first statement of the main() function implies that a variable emp of type employee_data is defined. This definition reserves 42 bytes of space in memory for the structure type variable emp that includes 30 bytes for the name, 4 bytes for the age, and 8 bytes for the salary (assuming we are working on a 32-bit machine). Sometimes, however, the definition can take more memory to align data bytes, which varies from compiler to compiler; this concept is called byte alignment.

Byte alignment is a very interesting feature. Most 16-bit and 32-bit processors do not allow words to be stored at any offset. Therefore, this is done as a part of the microprocessor design by taking advantage of byte alignment, where the processor reads and writes data from and into the memory cell at one go. Compilers also follow the byte alignment restrictions imposed by the target microprocessor. This means that the compiler has to pad extra bytes into the structure so that it does not violate any restriction imposed by the target microprocessor. Consider the following structure:

```cpp
struct Message
{
    short opcode;
    char subfield;
    long message_length;
    char version;
    short destination_processor;
};
```

For the preceding structure, the actual structure after byte alignment is as follows:

```cpp
struct Message
{
    short opcode;
    char subfield;
    char pad1;          // Pad to start the long word at a 4 byte boundary
    long message_length;
    char version;
    char pad2;          // Pad to start a short at a 2 byte boundary
    short destination_processor;
    char pad3[4];       // Pad to align the complete structure to a 16 byte boundary
};
```

Although, we have shown a preliminary example of byte alignment, it may vary from compiler to compiler. However, the basic idea of byte alignment is the same.

On line numbers 16, 18, and 20 of Listing 12.4, we prompt for the employee’s personal information from a user and save it in the data members of emp variable. This implies that employee name entered at line number 17 is saved in emp.employee_name; employee age entered at line number 19 is saved in emp.age; and employee salary entered at line number 21 is saved in emp.salary. Therefore, whenever we need to access inner data members of a structure type variable, we can use the dot operator. However, in case, we are dealing with the struct employee_data type’s pointer, for example,

```cpp
struct employee_data *ptr;
```

Then access to employee information is done with the indirect operator, that is, ->. In this case, we can access the information as ptr->employee_name, ptr->age, and ptr->salary.

Following is the output of Listing 12.4:

```text
Enter Employee Name: John
Enter Employee Age: 40
Enter Employee Salary: 16000
Employee John is 40 years old with Rs 16000 salary.
```

Now, we learn how to declare and define a structure variable at the same time. Consider the following code snippet:

```cpp
1:struct employee_data
2:{
3:    char employee_name[30];
4:    int age;
5:    double salary;
6:}emp;
```

In the preceding code snippet, line number 6 contains the definition to the structure variable emp. This is how we can combine both the declaration and the definition of a structure variable.
