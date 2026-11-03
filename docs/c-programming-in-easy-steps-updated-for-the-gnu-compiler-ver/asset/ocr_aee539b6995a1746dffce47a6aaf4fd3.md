# Describing dimensions

The numbering of array elements is more correctly known as the “array index” and, because element numbering starts at zero, is sometimes referred to as a “zero-based index”. An array created with a single index is a one-dimensional array in which the elements appear in a single row:

| Element content... | A | B | C | D | E |
| Index numbers... | [0] | [1] | [2] | [3] | [4] |

Arrays can also have multiple indices – to represent multiple dimensions. An array created with two indices is a two-dimensional array in which the elements appear in multiple rows:

| First index | [0] | A | B | C | D | E |
|  | [1] | F | G | H | I | J |
| Second index | [0] | [1] | [2] | [3] | [4] |

With multi-dimensional arrays the value contained in each element is referenced by stating the number of each index. For example, with the two-dimensional array above, the element at [1][2] contains the letter H.

Two-dimensional arrays are useful to store grid-based information, such as XY coordinates. Creating a three-dimensional array, with three indices, would allow XYZ coordinates to be stored:

![](bbox=[0.45, 0.68, 0.85, 0.92])

![](bbox=[0.08, 0.62, 0.18, 0.73])

Multi-dimensional arrays with more than two indices can produce hard-to-read source code and may lead to errors.

Additional indices allow the creation of arrays with many dimensions, but in reality multi-dimensional arrays of more than three indices are uncommon as they are difficult to envision.