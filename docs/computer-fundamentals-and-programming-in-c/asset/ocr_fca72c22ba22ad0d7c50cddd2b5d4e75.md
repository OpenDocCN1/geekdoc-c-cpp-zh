age, and salary. The name would have to be stored as a string, i.e., an array of characters terminated with an ASCII null character, and the age and salary would be integers. Hence, the only way one can work with this collection of data is as separate variables. This is not as convenient as a single data structure using a single name. Therefore, C provides a keyword struct, which is used to form a user-defined data type that can hold a collection of elements of different fundamental data types. This conglomerate of user-defined data type, is called a structure. At first, it is easier to think of this as a record, although it is a little more versatile than what it appears to be.

A structure is a collection of variables under a single name. These variables can be of different types, and each has a name which is used to select it from the structure. Therefore, a structure is a convenient way of grouping together several pieces of related information.

Thus, a structure can be defined as a new named type, thus extending the number of available data types. It can use other structures, arrays, or pointers as some of its members, though this can get complicated unless one is careful.

A structure provides a means of grouping variables under a single name for easier handling and identification. Complex hierarchies can be created by nesting structures.

Structures may be copied to and assigned. They are also useful in passing groups of logically related data into functions.

# ## 14.2.1 Declaring Structures and Structure Variables

A structure is declared by using the keyword struct followed by an optional structure tag followed by the body of the structure. The variables or members of the structure are declared within the body.

The general format of declaring a simple structure is given as follows.

```
```c
struct <structure_tag_name>{
<data_type member_name1>;
<data_type member_name2>;
:
} <structure_variable1>,<structure_variable2>,...;
```
```

The structure_tag_name is the name of the structure. The structure_variables are the list of variable names separated by commas. Each of these structure_variable names is a type of type structure_tag_name. The structure_variable is also known as an instance variable of the structure. Each member_name declared within the braces is called a member or structure element.

Like all data types, structures must be declared and defined. There are three different ways to declare and/or define a structure. These are:

+   - Variable structure
+   - Tagged structure
+   - Type-defined structure

A variable structure may be defined as follows.

```
```c
struct
{
member_list
}variable_identifier;
```
```

As an example the following statement is a definition of a variable structure:

```
```c
struct
{
int x;
int y;
}a;
```
```

It does not offer any advantage over other declaration formats. A tagged structure has been described earlier. It has the following format:

```
```c
struct tag_name
{
member_list
}variable_identifier;
```
```

The preceding structure declaration may be expressed as a tagged structure as follows:

```
```c
struct coordinate
{
int x;
int y;
}a;
```
```

This creates a structure variable named 'a' and has a separate instance of all members (x and y) in the structure coordinate. If one concludes the structure with a semicolon after the closing brace, no variable is defined. In this case, the structure is simply a type template with no associate storage. Once one has declared a tagged structure type, then the structure variable can be defined by specifying the following statement.

```
```c
struct tag_name variable1, variable2, ...;
```
```

Type-defined structures have been discussed later on (see Section 14.2.5).

The proper place for structure declarations is in the global area of the program before main(). This puts them within the scope of the entire program and is mandatory if the structure