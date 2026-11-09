You can navigate between records in simple data binding by using the **BindingContext** class. This class in Windows Forms application provides information about the binding and binding elements that are required to build the channel for data binding. The inheritance hierarchy of the **BindingContext** class is as follows:

```
System.Object
    System.Windows.Forms.BindingContext
```

The **BindingContext** object allows you to set the current record displayed in simple-bound controls, using the **Position** property. In simple words, it means that when a simple-bound control is bound to a field of a table, the object of the **BindingContext** class keeps track of the current record for the binding.

Perform the following steps to implement simple data binding using the **BindingContext** class:

+   1. *Drag and drop* the controls, listed in Table 5.2, on the Form1 form of the **SimpleDataBinding** application and also set their properties and values:

**Table 5.2: Displaying the Controls to be Added to the SimpleDataBinding Application**

| Controls | Name Property Value | Text Property Value |
|---|---|---|
| Button | button1 | << |
| Button | button2 | < |
| Button | button3 | > |
| Button | button4 | >> |

+   2. *Set* the Size property of the Form1 form to **424, 247**.
+   3. *Import* the **System.Data.SqlClient** namespace.
+   4. *Provide* the code for the Click event of the << button by *double-clicking* the << button at design time and *adding* the code, listed in Listing 5.2, in the Code Editor:

```
**Listing 5.2: Showing the Code to Display the First Record**

```csharp
private void button1_Click(object sender, EventArgs e)
{
    this.bindingContext[dataSet11, "Employees"].Position = 0;
}
```
```

In Listing 5.2, at the Click event of the **button1** button, the **BindingContext** class has a **Position** property set to 0 to display the first record of the dataset.

+   5. *Provide* the code for the Click event of the < button by *double-clicking* the < button at design time and *adding* the code, listed in Listing 5.3, in the Code Editor:

```
**Listing 5.3: Showing the Code to Display the Previous Record**

```csharp
private void button2_Click(object sender, EventArgs e)
{
    this.bindingContext[dataSet11, "Employees"].Position -= 1;
}
```
```

In Listing 5.3, at the Click event of the **button2** button, the **BindingContext** class has a **Position** property set to one less than the current position of the record to display the previous record of the dataset.

+   6. *Provide* the code for the Click event of the > button by *double-clicking* the > button at design time and *adding* the code, listed in Listing 5.4, in the Code Editor:

```
**Listing 5.4: Showing the Code to Display the Next Record**

```csharp
private void button3_Click(object sender, EventArgs e)
{
    this.bindingContext[dataSet11, "Employees"].Position += 1;
}
```
```

In Listing 5.4, at the Click event of the **button3** button, the **BindingContext** class has a **Position** property set to one more than the current position of the record to display the next record of the dataset.