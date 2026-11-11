Q2. How can you create structures in C++?

Ans. You can create a structure in C++ by declaring a structure with a structure name and different types of data members that can be stored in a structure. Next, you define structure variables for accessing data members of a structure.

You have to use the struct keyword just before the structure name. After specifying the structure name, the structure starts with the opening curly brace { and ends with the closing curly brace }. Further, a semicolon (;) must be placed after the closing curly brace. All the data members of a structure are specified between these braces.

Q3. Why do you create a variable of the structure? What are the types of variable you can declare for the structure? How can you create a variable?

Ans. First of all, you define a structure and its members by using the struct keyword. Once the structure is defined, the next step is to declare the structure variables, so that you can assign values to structure members and also use these values as and when required. A structure variable can be declared as global or as local. Declaring global variable implies that the scope of the structure variable is global, which can be used anywhere, throughout the C++ program. Generally, global variable are declared at the time of defining the structure. However, you also declare structure variables as local variables, which implies that such local variables are accessible within the specific part of the program. For example, if you have created a structure variable inside the function of the C++ program, then it can be accessed within the function body only and will be termed as a local variable.

Q4. How can you access and initialize structure members in C++?

Ans. Every structure has some elements known as members of the structure, which are declared within the body of the structure. When you define a structure, you can define members with a unique variable name. You can use the dot (.) operator between structure variable name and structure element (member of structure) to access and initialize a structure element. The syntax of accessing a structure element is as follows:

```
structure_variable_name.structure_element;
```

In the preceding code snippet the structure_variable_name is the variable of structure and the structure_element is the name of the structure member you want to access. Moreover, a dot (.) is placed between them so that the compiler can also understand the same.

Similarly, you can initialize structure elements by using the dot (.) operator as shown in following code snippet:

```
employee_one.name = "Mohan";
employee_one.age = 22;
```