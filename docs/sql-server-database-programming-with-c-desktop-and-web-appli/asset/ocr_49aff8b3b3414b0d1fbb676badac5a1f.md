# SelectWizard Project

# SQL Server Database Programming with C#

| cmdInsert_Click(object sender, EventArgs e) | cmdInsert_Click(object sender, EventArgs e) |

```
private void cmdInsert_Click(object sender, EventArgs e)
{
    int check = 0;
    CreateFacultyCollection();
    check = CheckFacultyCollection();
    if (check == 0)
        MessageBox.Show("Please fill all textboxes...");
    else
    {
        // continue to perform the data insertion...
        RemoveFacultyCollection();
    }
}
```

**FIGURE 6.3** The codes for the insert event procedure.

In order to use the collection to check one needs to add all TextBoxes into the collection object after the collection object FacultyCollection is created by using the Add() method. One point we need to emphasize is order to perform this validation. When the event starts, TextBoxes are blank. The user needs to enter all faculty information into the appropriate TextBox, and then click the Insert button to perform this data insertion. The time to add all TextBoxes into the collection object should be after the user has finished entering pieces of information into TextBoxes, not before. In addition, each time that the user finds validation by checking all TextBoxes, All TextBoxes should be removed from that since the collection only allows those TextBoxes to be added by one time.

Another point to be noted that in order to simplify this validation, in this application we need all TextBoxes to be filled with certain information or a NULL value needs to be entered if no information is available. In other words, do not allow any TextBox to be empty. The data insertion will not be performed until all TextBoxes are non-empty in this application.

Based on these descriptions, we need to create three user-defined methods to perform this addition, checking and removing TextBoxes from the collection object, respectively.

Open the graphical user interface (GUI) window of the Faculty Form, and double-click the Insert button to open its Click method. The codes that we are shown in Figure 6.3 into this method.

Let's look at this piece of code to see how it works.

+   A. We need to integrate an integer variable check and initialize it to zero. The purpose of using this variable is to hold the returned status of the execution of the method CheckFacultyCollection() later to update the validation for all TextBoxes is successful.

+   B. We need to call the CreateFacultyCollection() to add all TextBoxes into the collection FacultyCollection. Refer to Figure 6.4 for the detailed codes for this method.

+   C. We need to use the CheckFacultyCollection() method to validate whether all TextBoxes are non-empty. Refer to Figure 6.5 for the detailed codes for this method.

+   D. If the checking status returned from the CheckFacultyCollection() method is non-zero, which means that some TextBoxes are empty and that the validation has failed. A MessageBox() method is executed with a warning information to indicate this case.

+   E. Otherwise, if the returned status is zero, which means that all TextBoxes are filled with related information and this validation is successful, we need to build our codes to perform the data insertion process.