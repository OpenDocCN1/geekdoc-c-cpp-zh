# Declaring an Array

In C#, declare arrays using square brackets. First, you specify the element type of the array, followed by open and closed square brackets; then you enter the name of the variable. Listing 3.6 declares a variable called languages to be an array of strings.

LISTING 3.6: Declaring [] Array

```
string[] languages;
```

Obviously, the first part of the array identifies the data type of the elements within the array. The square brackets that are part of the declaration identify the rank, or the number of dimensions, for the array; in this case, it is an array of rank 1. These two pieces form the data type for the variable languages.

> Language Contrast: C++ and Java—Array Declaration
The squares for an array in C appear immediately following the data type instead of after the variable declaration. This practice keeps all type information together instead splitting it up before and after the identifier, as occurs in C++ and Java—with the latter also allowing the square brackets to appear either the data type or the variable name.

Listing 3.6 defines an array with a rank of 1. Commas within the square brackets define additional dimensions. Listing 3.7, for example, defines a two-dimensional array of cells for a game of chess or tic-tac-toe.

LISTING 3.7: Declaring a Two-Dimensional Array

```
// / | |
// --+-------
// /     |     |
// /   +-----+  /
int[,][] cells;
```

In Listing 3.7, the array has a rank of 2. The first dimension could correspond to cells going across and the second dimension to cells going down. Additional