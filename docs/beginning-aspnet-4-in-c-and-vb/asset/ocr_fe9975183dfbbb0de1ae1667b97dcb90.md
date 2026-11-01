The ProductDataTable class, derived from DataTable and implementing the IEnumerable interface, defines a private DataColumn instance for each of the columns within the table. These are initialized again from the constructor by calling the private InitClass() member. Each column is used by the DataRow class (which is described shortly):

```
```csharp
[global::System.Diagnostics.DebuggerNonUserCodeAttribute()]
[global::System.CodeDom.Compiler.GeneratedCodeAttribute("System.Data.Design.TypedDataSetGenerator", "4.0.0.0")]
[global::System.ComponentModel.Browsable(false)]
public int Count {
    get {
        return this.Rows.Count;
    }
}

// Other row accessors removed for clarity - there is one for each column
```
```

code download product.cs

Adding rows to the table is taken care of by the two overloaded (and significantly different) AddProductRow() methods. The first takes an already constructed DataRow and returns a void. The second takes a set of values, one for each of the columns in the DataTable, constructs a new row, sets the values within this new row, adds the row to the DataTable object, and returns the row to the caller. Such widely different functions shouldn't really have the same name!

```
```csharp
[global::System.Diagnostics.DebuggerNonUserCodeAttribute()]
[global::System.CodeDom.Compiler.GeneratedCodeAttribute("System.Data.Design.TypedDataSetGenerator", "4.0.0.0")]
public ProductRow AddProductRow(string ProductName, int SupplierID,
    int CategoryID, string QuantityPerUnit, decimal UnitPrice,
    short UnitsInStock, short UnitsOnOrder, short ReorderLevel,
    bool Discontinued) {
    ProductRow rowProductRow = ((ProductRow) (this.NewRow()));
    object[] columnValuesArray = new object[] {
        null,
        ProductName,
        SupplierID,
        CategoryID,
        QuantityPerUnit,
        UnitPrice,
        UnitsInStock,
        UnitsOnOrder,
        ReorderLevel,
        Discontinued};
    rowProductRow.ItemArray = columnValuesArray;
    this.Rows.Add(rowProductRow);
    return rowProductRow;
}
```
```

code download product.cs

Just like the InitClass() member in the DataSet-derived class, which added the table into the DataSet class, the InitClass() member in ProductDataTable adds columns to the DataTable class. Each column's properties are set as appropriate, and the column is then appended to the columns collection:

```
```csharp
[global::System.Diagnostics.DebuggerNonUserCodeAttribute()]
[global::System.CodeDom.Compiler.GeneratedCodeAttribute("System.Data.Design.TypedDataSetGenerator", "4.0.0.0")]
private void InitClass() {
    this.columnProductID = new
    global::System.Data.DataColumn("ProductID",
    typeof(int), null, global::System.Data.MappingType.Element);
    base.Columns.Add(this.columnProductID);
```
```