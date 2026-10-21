# Customizing Header Cells

The `InheritedStyle` property value for each header cell in the control is determined by considering the values of following properties in sequence:

+   - The `Style` property for the `DataGridViewCell` object that represents the cell.
+   - The `ColumnHeadersDefaultCellStyle` property or the `RowHeadersDefaultCellStyle` property for the control object.
+   - The `DefaultCellStyle` property for the control object.

So if the `Style` property value for the cell object has been set, the `InheritedStyle` property for the cell takes this value and determines the appearance of the cell. If not, the next candidate takes effect if the value for that has been set. If the second choice has not been set, the `DefaultCellStyle` property for the control is applied.

Don’t forget that the value of the `InheritedStyle` property is an object of type `DataGridViewCellStyle`, which itself has properties that determine various aspects of the appearance of the cell. The process of going through the priority sequence applies to each of the properties of the `DataGridViewCellStyle` object, so overall there may be contributions from more than one of the properties in the priority sequence.

# Customizing Non-Header Cells

The `InheritedStyle` property value for each non-header cell in the control (the non-header cells being the cells containing data) is determined from the following properties in the `DataGridView` object in sequence:

+   - The `Style` property for the `DataGridViewCell` object that represents the cell.
+   - The `DefaultCellStyle` property for the `DataGridViewRow` object that represents the row containing the cell. You would typically reference the `DataGridViewRow` object by indexing the `Rows` property for the control object.
+   - The `AlternatingRowsDefaultCellStyle` property for the control object; this applies only to cells in rows with odd index numbers.
+   - The `RowsDefaultCellStyle` property for the control object.
+   - The `DefaultCellStyle` property for the `DataGridViewColumn` object that contains the cell. You would typically access a `DataGridViewColumn` object by indexing the `Columns` property for the control object.
+   - The `DefaultCellStyle` property for the control object.

Potentially you could have a different `DataGridViewCellStyle` object for each cell, but for efficiency you need to keep the number of such objects to a minimum.

The next Try It Out explores some of these possibilities in an example where you set up the `DataGridView` object yourself.