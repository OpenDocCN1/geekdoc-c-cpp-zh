```
Case Windows.Forms.DialogResult.Cancel
    e.Cancel = True
End Select
End If
```

# Run the Application

STEP 1: Very cautiously, run the application. We want to try editing existing records and adding new sales and stores, but the Pubs database has many constraints and we have not yet added validation and exception handling.

STEP 2: Make a change to the information of an existing store and move to another record. When you move back to the changed record, the change should still be showing.

STEP 3: Add a new sale for an existing store. Be aware that all fields are required for a sale record, so you must enter something in every cell. You must add a title_id for a title that exists in the titles table, so for now use "BU1032" for testing. We will take care of this problem shortly. Unless you are very careful, you will likely generate constraint violations. We will add validation and exception handling soon.

STEP 4: Click the Save button on the navigation bar. If you didn’t violate any of the database constraints, the database should save.

STEP 5: Assuming that you were able to save the database successfully, close the application and run it again. Check for your changes. If you were unable to save, try making less drastic changes and save again. If you have made unwanted changes to the database, you can delete the file in the bin\Debug folder. On the next program run, a fresh copy of the database will be copied to the folder.

# Help the User Enter Valid Data

You can take some simple steps to help the user enter valid data.

STEP 1: In the Form Designer, set the Stor_idTextBox to ReadOnly. This will prevent the user from changing the store’s primary key field. Later we will set it back for adding a new store.

STEP 2: Open the DataSet Designer and check the MaxLength property of each of the text fields in both tables. Note that the date and quantity fields in the sales table do not have a MaxLength. Take notes for each field so you can set the MaxLength properties of all of the controls.

STEP 3: Switch back to the Form Designer and set the MaxLength property of each of the text boxes for the store table. You want to set the Stor_idTextBox also, as the user will be entering a stor_id for any new stores. Make these settings for the text boxes:

| stor_id | 4 |
| stor_name | 40 |
| stor_address | 40 |
| city | 20 |
| state | 2 |
| zip | 5 |