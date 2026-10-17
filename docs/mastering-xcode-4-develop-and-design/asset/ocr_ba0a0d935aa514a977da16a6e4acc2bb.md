![](bbox=[0.13, 0.17, 0.51, 0.43])

FIGURE 10.14 TestApp with its new to-do feature

# TAKING THE UI FOR A TEST-DRIVE

TestApp is ready for a test-drive. Build and run the application. Click the Add button to add a to-do item. Set a date (using the M/D/YY format you chose in the formatter’s attributes) and a description. Quit the application and relaunch. You’ll notice that the changes were automatically persisted. Now try sorting the table by clicking either of the column headers, and then try removing an item. Figure 10.14 shows TestApp in action.

It’s just as easy to add another attribute to the ToDoItem entity. To-dos need a completion check box. To do this, you could add a completed Boolean attribute to the ToDoItem entity and add another table column with a check box cell.