# 506 Appendix B Solutions to Exercises

The following AddEntries method copies entries from the two lists from_entry1
and from_entry2 into the result list to_entry:

```
// Add the entries in the two lists from_entry1 and from_entry2
// and save the sums in the destination entry list after to_entry.
AddEntries(ArrayEntry: from_entry1, ArrayEntry: from_entry2,
ArrayEntry: to_entry)
// Repeat as long as each list has items.
While (from_entry1 != null && (from_entry2 != null))
// Make the new entry.
to_entry.NextEntry = new ArrayEntry
to_entry = to_entry.NextEntry
to_entry.NextEntry = null

// See which column number is smaller.
If (from_entry1.ColumnNumber < from_entry2.ColumnNumber) Then
// Copy the from_entry1 entries.
to_entry.ColumnNumber = from_entry1.ColumnNumber
to_entry.Value = from_entry1.Value
from_entry1 = from_entry1.NextEntry
Else If (from_entry2.ColumnNumber < from_entry1.ColumnNumber)
Then
// Copy the from_entry2 entries.
to_entry.ColumnNumber = from_entry2.ColumnNumber
to_entry.Value = from_entry2.Value
from_entry2 = from_entry2.NextEntry
Else
// The columns number are the same. Add both entries.
to_entry.ColumnNumber = from_entry1.ColumnNumber
to_entry.Value = from_entry1.Value + from_entry2.Value
from_entry1 = from_entry1.NextEntry
from_entry2 = from_entry2.NextEntry
End If

// Add the rest of the entries from the list that is not empty.
if (from_entry1 != null) CopyEntries(from_entry1, to_entry)
if (from_entry2 != null) CopyEntries(from_entry2, to_entry)
EndEntries
```

This code loops through both "from" lists, adding the next entry from each list that has the smaller column number. If the current entries in each list have the same column number, the code creates a new entry and adds the values of "from" lists.

The following code shows how the Add method uses CopyEntries to add two matrices:

```
// Add two SparseArray matrices.
SparseArray: Add(SparseArray: array1, SparseArray: array2)
SparseArray: result = new SparseArray
```