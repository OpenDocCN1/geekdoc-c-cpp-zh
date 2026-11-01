![](bbox=[0.28, 0.11, 0.72, 0.34])

Figure 15.19. The updated data shown in the ListBox

# 15.3. Adding/Updating/Deleting Database Entries from our C# Program

We have manipulated data of the database in Access and displayed the updated data in our program. The problem is that the user may not have Access installed on his/her computer or we may need to manipulate entries of our database in a systematic way in our program. Adding new data, removing entries or updating data are all possible in our own program using the corresponding commands for the OleDBCommand object. Let’s start developing our example project for learning how we can manipulate database entries.

+   1. Create a new C# project.
+   2. Add six TextBoxes, six Labels, four Buttons and a ListBox on the form in the following layout shown in Figure 15.20.
+   3. Set the Names of the TextBoxes from top to down as insertNameTextBox, insertSurnameTextBox, insertAgeTextBox, updateNameTextBox, updateSurnameTextBox and updateAgeTextBox, respectively (confusing, I know!).
+   4. Set the Names of the Buttons as insertButton, updateButton, listButton and deleteButton in order.
+   5. Set the Texts of the Buttons as Insert, Update, List entries and Delete selected, respectively.
+   6. Set the Texts of the Labels as Name:, Surname:, Age:, Name:, Surname: and Age:, respectively.
+   7. Finally, set the Name of the ListBox as displayListBox. The form will look as in Figure 15.21 after these modifications.