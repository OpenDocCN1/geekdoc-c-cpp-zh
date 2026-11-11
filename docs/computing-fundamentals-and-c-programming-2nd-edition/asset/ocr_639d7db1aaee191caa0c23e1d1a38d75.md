In defining a structure you may note the following syntax:

+   1. The template is terminated with a semicolon.
+   2. While the entire definition is considered as a statement, each member is declared independently for its name and type in a separate statement inside the template.
+   3. The tag name such as **book_bank** can be used to declare structure variables of its type, later in the program.

# ### 12.2.1 Arrays vs Structures

Both the arrays and structures are classified as structured data types as they provide a mechanism that enable us to access and manipulate data in a relatively easy manner. But they differ in a number of ways which are as follows:

+   1. An array is a collection of related data elements of same type. Structure can have elements of different types.
+   2. An array is derived data type whereas a structure is a programmer-defined one.
+   3. Any array behaves like a built-in data type. All we have to do is to declare an array variable and use it. But in the case of a structure, first we have to design and declare a data structure before the variables of that type are declared and used.

# ## 12.3 DECLARING STRUCTURE VARIABLES

After defining a structure format we can declare variables of that type. A structure variable declaration is similar to the declaration of variables of any other data types. It includes the following elements:

+   1. The keyword **struct**.
+   2. The structure tag name.
+   3. List of variable names separated by commas.
+   4. A terminating semicolon.

For example, the statement

```
```c
struct book_bank, book1, book2, book3;
```
```

declares **book1**, **book2**, and **book3** as variables of type **struct book_bank**.

Each one of these variables has four members as specified by the template. The complete declaration might look like this:

```
```c
struct book_bank
{
    char    title[20];
    char    author[15];
    int     pages;
    float   price;
};
struct book_bank book1, book2, book3;
```
```

Remember that the members of a structure themselves are not variables. They do not occupy any memory until they are associated with the structure variables such as **book1**. When the compiler comes