# Part VII: Advanced Access Programming Techniques

Access always confirms deletions initiated by the user. Access displays a message box asking the user to confirm the deletion. If the user affirms the deletion, the current record is removed from the form's recordset and temporarily stored in memory so that the deletion can be undone if necessary. The AfterDelConfirm event occurs after the user confirms or cancels the deletion. If the BeforeDelConfirm event isn't canceled, the AfterDelConfirm event occurs after the delete confirmation dialog box is displayed. The AfterDelConfirm event occurs even if the BeforeDelConfirm event is canceled.

# FIGURE 28.12

Recalculating a control after a record is deleted.

![](bbox=[0.2, 0.45, 0.6, 0.75])

The AfterDelConfirm event procedure returns status information about the deletion. Table 28.2 describes the deletion status values.

# TABLE 28.2 Deletion Status Values

| Status value | Description |
|---|---|
| acDeleteOK | Deletion occurred normally. |
| acDeleteCancel | Deletion canceled programmatically. |
| acDeleteUserCancel | User canceled deletion. |

The Status argument for the AfterDelConfirm event procedure can be set to any of these values within the procedure. For example, if the code in the AfterDelConfirm event procedure determines that deleting the record may cause problems in the application, the Status argument should be set to acDeleteCancel:

```
If <Condition_Indicates_a_Problem> Then
    Status = acDeleteCancel
```