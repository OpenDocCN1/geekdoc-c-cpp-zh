# 14.6 Updating Sequential Files

Data that is formatted and written to a sequential file as shown in **Section 14.3** cannot be modified without the risk of destroying other data in the file. For example, if the name “`White`” needs to be changed to “`Worthington`,” the old name cannot be overwritten without corrupting the file. The record for `White` was written to the file as

```
```text
300 White 0.00
```
```

If this record were rewritten beginning at the same location in the file using the longer name, the record would be

```
```text
300 Worthington 0.00
```
```

The new record contains six more characters than the original record. Therefore, the characters beyond the “h” in “`Worthington`” would overwrite the `0.00` and the beginning of the next sequential record in the file. The problem is that, in the formatted input/output model using the stream insertion operator `<<` and the stream extraction operator