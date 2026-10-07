# ASP.NET Web Services

Let's take a closer look at this piece of codes to see how it works.

+   A. Eight default members are added to the combobox control ComboName using the Add() method, and this will allow users to select one desired faulty from this combobox control to perform the data query over the project runs. The default-selected faulty is the first one by setting the SelectedIndex to zero.
B. Three methods are also added into another combobox control ComboMethod to allow users of one to perform the associated data query via our Web service. The default method is selected as the first one.

Next let's develop the codes for the Back button's Click method.

# 9.3.10.3.2 Develop Codes for the Back Click Method

This coding is very easy; just open the Back click's method by double-clicking it from the Form Window and enter the following one line code into this:

```
Application.Exit();
```

The purpose of this coding line is to terminate our project as this button is clicked by the user. Next let's build the codes for the Select button's Click method.

# 9.3.10.3 Develop the Codes for the Select Button Click Event Procedure

Open the Select button's click method and enter the codes that are shown in Figure 9.34 into this method. Let's have a closer look at this piece of codes to see how it works.

+   A. Some data objects are created at the beginning of this method, which include a Web Service SQLResult is created using the protocol given above, a new object SQLResult as a mapping of the real SQLResult developed in

| WinSelectProject | cmdSelect_Click(object sender, EventArgs e) |
|---|---|
| A | void cmdSelect_Click(object sender, EventArgs e) {

  SQLSelect.WebServiceSelect wsSelect = new SQLSelect.WebServiceSelect();
  SQLSelect.SQLResult wsResult = new WS_SQLSelect.SQLResult();
  DataSet wsData = new DataSet(null);

  if (ComboMethod.Text == "Object Method") {
    try(wsResult = SQLSelect.GetSelectObject(ComboName.Text));
    catch (Exception err) { MessageBox.Show("Web service is wrong: " + err.Message); }
    ProcessObject(ref wsResult);
  } else if (ComboMethod.Text == "Stored Procedure Method") {
    try { wsResult = SQLSelect.GetSelectSP(ComboName.Text); }
    catch (Exception err) { MessageBox.Show("Web service is wrong: " + err.Message); }
    ProcessObject(ref wsResult);
  } else {
    try { wsData = SQLSelect.GetSelectDataSet(ComboName.Text); }
    catch (Exception err) { MessageBox.Show("Web service is wrong: " + err.Message); }
    FillDataDataSet(ref wsData);
  }
} |

FIGURE 9.34 The codes for the select button method.