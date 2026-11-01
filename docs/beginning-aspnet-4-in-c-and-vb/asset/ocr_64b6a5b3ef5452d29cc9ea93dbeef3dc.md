# Updating an Existing Row

Updating an existing row within the DataTable is just a case of using the DataRow class's indexer with either a column name or column number, as shown in the following code:

```
r["RegionDescription"]="North West England";
r[1] = "North West England";
```

Both of these statements are equivalent (in this example):

```
Changed RegionID 5 description
1  Eastern          Unchanged
2  Western          Unchanged
3  Northern         Unchanged
4  Southern         Unchanged
5  North West England Modified
```

Prior to updating the database, the row updated has its state set to Modified as shown.

# Deleting a Row

Deleting a row is a matter of calling the Delete() method:

```
r.Delete();
```

A deleted row has its row state set to Deleted, but you cannot read columns from the deleted DataRow because they are no longer valid. When the adaptor's Update() method is called, all deleted rows will use the DeleteCommand, which in this instance executes the RegionDelete stored procedure.

# Writing XML Output

As you have seen already, the DataSet class has great support for defining its schema in XML, and just as you can read data from an XML document, you can also write data to an XML document.

The DataSet.WriteXml() method enables you to output various parts of the data stored within the DataSet. You can elect to output just the data, or the data and the schema. The following code shows an example of both for the Region example shown earlier:

```
ds.WriteXml("..\\WithoutSchema.xml");
ds.WriteXml("..\\WithSchema.xml", XmlWriteMode.WriteSchema);
```

The first file, WithoutSchema.xml, is shown here:

```
<?xml version="1.0" standalone="yes"?>
<NewDataSet>
<Region>
<RegionID>1</RegionID>
<RegionDescription>Eastern</RegionDescription>
</Region>
<Region>
<RegionID>2</RegionID>
<RegionDescription>Western</RegionDescription>
</Region>
<Region>
<RegionID>3</RegionID>
<RegionDescription>Northern</RegionDescription>
</Region>
<Region>
<RegionID>4</RegionID>
<RegionDescription>Southern</RegionDescription>
</Region>
</NewDataSet>
```