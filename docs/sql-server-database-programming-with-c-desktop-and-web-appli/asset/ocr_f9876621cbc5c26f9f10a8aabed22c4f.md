# Data Upating and Deleting with Visual C#.

![](bbox=[0.118, 0.089, 0.882, 0.269])

**FIGURE 7.34** The created stored procedure.

The only input parameter to this stored procedure is a **faculty_name**, which can be obtained from the Faculty Name combobox in the Faculty Form. The only point to note is that this input dynamic parameter or faculty name must be identical with one we used for the coding line of adding this parameter in the Delete's Click method, which is @fname, as shown in Figure 7.32.

The function of this stored procedure is straightforward. A SQL query is executed to remove a selected faculty record from the **Faculty** table in our sample database with a selected faculty name, indicated by the input parameter @fname.

Click on the **Update** icon located at the upper-left corner, as shown in Figure 7.34, to save this stored procedure into our database. After the opened **Preview Database Updates** wizard, click on the **Update** database, a successful updating message should be displayed in the **Data Tools Operations** wizards located at the bottom.

Next's run our Visual C# project to collect all stored procedures to perform data updating and deleting actions for the faculty table in our sample database.

# 7.5.1.3  Call the Stored Procedures to Perform Data Updating and Deleting Actions

Run our project by clicking the Start button, enter a suitable username and password to complete the login process, and then select the **Faculty Information** item from the Selection Form to open the Faculty Form window. Select the faculty name **Ying Bai** from the Faculty Name combobox, and click the **Select** button to get and display the information for the selected faculty.

To update this faculty record, enter the following data into the associated texts to perform this data updating:

| Faculty Name | Susan Bai |
| --- | --- |
| Title | Professor |
| Office | HTC-218 |
| Phone | 750-378-2800 |
| College | Duke University |
| Email | sbai@college.edu |

Click on the **Update** button in the Faculty Form window to update this record. After the opened File Selection wizard, browse to your local folder where all faculty image files are located, select a desired faculty image file, **White.jpg**, and click on the **Open** button to perform this data updating action.

To validate this data updating, select another faculty from the combobox and click the **Select** button to retrieve back information for that faculty. Then go to the Faculty Name combobox again, and one can find that the updated faculty member, **Susan Bai**, is in there.