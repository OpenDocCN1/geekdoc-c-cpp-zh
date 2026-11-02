
slicing operation accesses an array. So while the expressions Inventory (5) and Inventory (5 .. 5) are very similar, their result types are very different. Inventory (5) is a natural number, whereas Inventory (5 .. 5) is an array consisting of one natural number.

Our slicing examples also illustrate the sliding feature of array assignment. The index ranges of the source and target of these assignments are different. The ten values in the source array slide into the target array. The range of the indices of the source and target may be different. The two restrictions for array assignment are that the target and source be the same type and that the number of components is the same.

We define multidimensional arrays by defining multiple indices. The following examples illustrate two ways to define an array in which we use two indices to locate a component:

```ada
type Row_Index is range 1 .. 1000;
type Col_Index is range -5 .. +5;
```

```ada
type Two_D_Array is array (Row_Index, Col_Index) of Float;
```

```ada
type One_Row       is array (Col_Index) of Float;
type Another_2D_Array is array (Row_Index) of One_Row;
```

```ada
Canary : Two_D_Array;       -- A 2-dimensional array variable
Finch  : Another_2D_Array; -- An array of arrays variable
```

The syntax for indexing a two-dimensional array is different from that for indexing an array of arrays. Here are examples of each kind:

```ada
-- Assign zero to row 12, column 2 of the 2-D array
Canary (12, 2) := 0.0;
```

```ada
-- Assign zero to the second component of the 12th array
Finch (12)(2) := 0.0;
```

Slicing is limited to one-dimensional arrays. We cannot slice the array variable Canary. However, we can slice an array in our array of arrays variable Finch.

## Constrained and Unconstrained Array Types

All the previous array examples were of constrained arrays. A constrained array type is an array type for which there is an index range constraint. An unconstrained array type definition provides only the type of the index, it does not specify the range of that type. Here is an example:

```ada
type Float_Array is array (Positive range <>) of Float;
```

This statement defines the unconstrained array type Float_Array. The components of this array type are type Float and the index of this array is subtype Positive. We did not specify the range of the positive index. The box symbol, <>, indicates that this is the definition of an unconstrained array type. Because there is no range constraint for this array type, we cannot use an unconstrained array type to declare an array variable because the compiler cannot determine how much memory to allocate to such an array variable.

```ada
Illegal : Float_Array; -- This declaration will not compile
```

The two important uses of unconstrained array types are (a) as a base for a constrained array subtype and (b) for the type of a formal parameter. Here are examples of constrained array subtypes:

```ada
subtype Small_Array is Float_Array (1 .. 10);
subtype Large_Array is Float_Array (1000 .. 9999);
```

```ada
Small : Small_Array; -- An array of 10 Float values
Large : Large_Array; -- An array of 9,000 Float values
```

Because the arrays Small and Large have the same base type, we can combine them in expressions like these:

```ada
Large (1001 .. 1010) := Small;      -- Copy 10 values
if Small /= Large (2001 .. 2010) then -- Compare 10 values
   -- Copy 21 values
   Large (2001 .. 2021) := Small & 14.2 & Small;
end if;
```

The second assignment statement in the preceding example illustrates another array operation, concatenation. The & operator may be used to concatenate two arrays, an array and a component, or two components. The result in all cases is an array. In our example, we created a 21 component array by concatenating a copy of array Small with the value 14.2 and a second copy of Small.

Here is an example of a subprogram specification with an unconstrained array parameter:

```ada
function Average (Values : in Float_Array) return Float;
```

The formal parameter Values will match any actual parameter that is a constrained array subtype of Float_Array. The formal parameter will take on the index constraint of the actual parameter. Here are some calls to function Average using our two previously defined array variables:

```ada
Avg := Average (Small);       -- Average of 10 values
Avg := Average (Large);       -- Average of 9,000 values
Avg := Average (Large (2001 .. 2010)); -- Average of 10 values
Avg := Average (Large & Small);      -- Average of 9,010 values
```

### Array Attributes

As you just saw, we can pass different size arrays to function Average. We do not need to pass the size of the array or its starting or ending indices. The function makes use of attributes to obtain the properties of the actual array parameter. Earlier we introduced some of the most commonly used attributes for discrete types. There are attributes for array types as well. The attributes most commonly used with arrays are as follows:

| Attribute | Description |
| --- | --- |
| `'First` | Returns the lower bound of the index range |
| `'Last` | Returns the upper bound of the index range |
| `'Length` | Returns the number of components in the array |
| `'Range` | Returns the index range of the array (`'First .. 'Last`) |

Here is the body of function Average, which uses two of these attributes:

```ada
function Average (Values : in Float_Array) return Float is
    Sum : Float;
begin
    Sum := 0.0;
    for Index in Values'Range loop
        Sum := Sum + Values (Index);
    end loop;
    return Sum / Float (Values'Length);
end Average;
```

When working with unconstrained array parameters, you should not make any assumptions about the first or last index values. Although many arrays use 1 as a starting index, you should use the attributes rather than make such an assumption.

Section 3.6 of the ARM (2012) provides the details on array types and attributes. There you may also find how to use attributes with multidimensional arrays.

### Array Aggregates

An array aggregate is a collection of components enclosed in parentheses. One might think of an array aggregate as an array literal. Aggregates are commonly used to initialize array objects. Here are some examples of using array aggregates to initialize the array variable Small defined earlier:

```ada
Small := (0.0, 1.0, 2.0, 3.0, 4.0, 5.0, 4.0, 3.0, 2.0, 1.0);  -- by position
Small := (1 .. 10 => 0.0);                                      -- by name
Small := (1 .. 5 => 0.0, 6 .. 10 => 1.0);
Small := (1 | 3 | 5 | 7 | 9 => 0.0, others => 1.0);
Small := (others => A + Sqrt (B));
```

In the first example, the ten components assigned to the array Small are given by position: 0.0 is assigned to Small(1), 1.0 is assigned to Small(2), and so on. In the other examples, we use array indices as names to assign values to specific locations within the array. Similar to the case selector, we can use ranges and individual index values separated by vertical bars to associate locations with values. The others keyword may be used last to associate a value with locations not previously specified. The last example, which calculates a value from the variables A and B, demonstrates that aggregates are not true literals, but simply collections of components.

Array aggregates are available for multidimensional arrays. Let us look at an example. Here is a two-dimensional array of integers with three rows indexed from -1 to 1 and four columns indexed from 1 to 4:

```ada
type Row_Range is range -1 .. 1;
type Col_Range is range 1 .. 4;
type Table_Array is array (Row_Range, Col_Range) of Integer;

Table : Table_Array;   -- 2-dimensional array with 12 elements
```

And here are examples of using aggregates to assign values to Table:

```ada
-- Assign all elements by position
Table := ((1, 2, 3, 4),
          (5, 6, 7, 8),
          (9, 8, 7, 6));
-- Assign rows by name, columns by position
Table := (-1 => (1, 2, 3, 4),
           0 => (5, 6, 7, 8),
           1 => (9, 8, 7, 6));
-- Assign all elements by name
Table := (-1 => (1 .. 4 => 2),
           0 => (1 .. 3 => 3, 4 => 6),
           1 => (2 => 5, others => 7));
Table := (-1 .. 1 => (1 .. 4 => 0));
Table := (others => (others => 0));
```
