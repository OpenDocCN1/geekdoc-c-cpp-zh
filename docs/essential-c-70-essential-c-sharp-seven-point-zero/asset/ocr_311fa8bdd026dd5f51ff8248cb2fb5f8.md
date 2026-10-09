# LISTING 3.8: Array Assignment Following Declaration

```
string[] languages;
languages = new string[]{"C#", "COBOL", "Java",
"C++", "Visual Basic", "Pascal",
"Fortran", "Lisp", "J#"};
```

Starting in C# 3.0, specifying the data type of the array (string) following new is optional as long as the compiler is able to deduce the element type of the array from the types of the elements in the array initializer. The square brackets are still required.

C# also allows use of the new keyword as part of the declaration statement, so it allows the assignment and the declaration shown in Listing 3.9.

# LISTING 3.9: Array Assignment with new during Declaration

```
string[] languages = new string[]{
"C#", "COBOL", "Java",
"C++", "Visual Basic", "Pascal",
"Fortran", "Lisp", "J#"};
```

The use of the new keyword tells the runtime to allocate memory for the data type. It instructs the runtime to instantiate the data type—in this case, an array.

Whenever you use the new keyword as part of an array assignment, you may also specify the size of the array within the square brackets. Listing 3.10 demonstrates this syntax.

# LISTING 3.10: Declaration and Assignment with the new Keyword

```
string[] languages = new string[9]{
"C#", "COBOL", "Java",
"C++", "Visual Basic", "Pascal",
"Fortran", "Lisp", "J#"};
```

The array size in the initialization statement and the number of elements contained within the curly braces must match. Furthermore, it is possible to assign an array but not specify the initial values of the array, as demonstrated in Listing 3.11.

# LISTING 3.11: Assigning without Literal Values

```
string[] languages = new string[9];
```