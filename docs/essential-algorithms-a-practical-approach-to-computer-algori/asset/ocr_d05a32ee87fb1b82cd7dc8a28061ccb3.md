# 92 Chapter 4 Arrays

to see how "wide" the array must be in that dimension, and then multiply the
resulting "widths" together:

```
Integer: ArraySize(Integer: lower_bounds[], Integer: upper_bounds[])
Integer: total_size = 0
For i = 0 To lower_bounds.Length - 1
  total_size = total_size * (upper_bounds[i] - lower_bounds[i])
Next i
  Return total_size
```

The next step, mapping row and column to a position in the one-dimensional
array, is a bit more confusing. Recall how the preceding mapped row
and column to an index in the values array. First the code defined how
complete rows belongs in the array and multiplied by the number of
items in a row. The code added 1 for each position in the item's
row that was before the item.

Moving to three dimensions isn't much harder. Figure 4-3 shows a 4x4x3
three-dimensional array with dimensions labeled height, row, and column.
entry with coordinates (1, 1, 3) is highlighted in gray.

![](bbox=[0.137, 0.442, 0.778, 0.622])

**Figure 4-3:** The first step in mapping an item to the values array is determining how
complete "slices" come before it.

To map the item's coordinates (1, 1, 3) to an index in the values array, first
determine how many complete "slices" come before it. Because the item's
height coordinate is 1, there is one complete slice before the item in the array.
The size of a slice is <row size> x <column size>. If the item has coordinates
(h, r, c), the number of items that come before this one to slices is given by
the following:

```
index = h x <row size> x <column size>
```

Next you need to determine how many items come before this one due to
rows. In this example, the item's row is 1, so one row comes before
the item in the values array. If the item has row r, you need to add r times the
size of a row to the index:

```
index = index + r x <row size>
```