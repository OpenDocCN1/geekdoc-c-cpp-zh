```
"Fortran", "Lisp", "J#");
// Retrieve 3rd item in Languages array (Java)
string language = languages[4];
```

The square bracket notation is also used to store data into an array. Listing 2.44 switches the order of "C++" and "Java".

# LISTING 2.44: Swapping Data between Positions in an Array

```
string[] languages = new string[9]{
    "C#", "COBOL", "Java",
    "C++", "Visual Basic", "Pascal",
    "Fortran", "Lisp", "J#"};
// Save "C++" to variable called Language.
string language = languages[3];
// Assign "Java" to the C++ position.
Languages[3] = languages[2];
// Assign language to location of "Java".
languages[2] = msg;
```

For multidimensional arrays, an element is identified with an index for each dimension, as shown in Listing 2.45.

# LISTING 2.45: Initializing a Two-Dimensional Array of Integers

```
int[,] cells = {
    {1, 0, 2},
    {0, 2, 0},
    {1, 2, 1}
};
// Set the winning tic-tac-toe move to be player 1.
cells[1,0] = 1;
```

Jagged array element assignment is slightly different because it is consistent with the jagged array declaration. The first element is an array within the array of arrays. The second index specifies the item within the selected array element (see Listing 2.46).

# LISTING 2.46: Declaring a Jagged Array

```
int[][] cells = {
    new int[]{1, 0, 2},
    new int[]{0, 2, 0},
    new int[]{1, 2, 1}
};
cells[1][0] = 1;
// ...
```