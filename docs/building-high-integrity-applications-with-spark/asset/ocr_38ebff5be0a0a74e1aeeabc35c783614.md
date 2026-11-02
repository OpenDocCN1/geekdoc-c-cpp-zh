slicing operation accesses an array. So while the expressions Inventory (5) and Inventory (5..5) are very similar, their result types are very different. Inventory (5) is a natural number, whereas Inventory (5..5) is an array consisting of one natural number.

Our slicing examples also illustrate the sliding feature of array assignment. The index ranges of the source and target of these assignments are different. The ten values in the source array slide into the target array. The range of the indices of the source and target may be different. The two restrictions for array assignment are that the target and source be the same type and that the number of components is the same.

We define multidimensional arrays by defining multiple indices. The following examples illustrate two ways to define an array in which we use two indices to locate a component:

```
type Row_Index is range 1 .. 1000;
type Col_Index is range -5 .. +5;
```

```
type Two_D_Array is array (Row_Index, Col_Index) of Float;
```

```
type One_Row       is array (Col_Index) of Float;
type Another_2D_Array is array (Row_Index) of One_Row;
```

```
Canary : Two_D_Array;       -- A 2-dimensional array variable
Finch  : Another_2D_Array; -- An array of arrays variable
```

The syntax for indexing a two-dimensional array is different from that for indexing an array of arrays. Here are examples of each kind:

```
-- Assign zero to row 12, column 2 of the 2-D array
Canary (12, 2) := 0.0;
```

```
-- Assign zero to the second component of the 12th array
Finch (12)(2) := 0.0;
```

Slicing is limited to one-dimensional arrays. We cannot slice the array variable Canary. However, we can slice an array in our array of arrays variable Finch.

# Constrained and Unconstrained Array Types

All the previous array examples were of constrained arrays. A constrained array type is an array type for which there is an index range constraint. An