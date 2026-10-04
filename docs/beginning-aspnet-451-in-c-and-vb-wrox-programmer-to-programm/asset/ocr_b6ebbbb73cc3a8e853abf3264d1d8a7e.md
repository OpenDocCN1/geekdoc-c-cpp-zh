With this toolbar, click the Show Diagram pane, the Show Criteria pane, and the Show SQL pane buttons to open their respective windows. The first four buttons on the toolbar should now be in a pressed state and the Document Window is split in four regions, with each region corresponding to one of the buttons on the toolbar. Figure 12-10 shows the entire Document Window with the four panes.

![](bbox=[0.118, 0.211, 0.715, 0.49])

FIGURE 12-10

The SQL pane displays the SQL statement that is used to retrieve the genres that are displayed in the Results pane. In this case, the SQL statement reads SELECT TOP (200) Id, Name, SortOrder FROM Genre to retrieve all columns and the first 200 rows from the table, but you can easily change that.

+   3. In the SQL pane, modify the query as follows:
SELECT Id, Name, SortOrder FROM Genre WHERE Id > 4\4. To make sure the SQL statement is valid, click the Verify SQL button to fix any errors your SQL statement may contain. Click the Execute SQL button (the one with the red exclamation mark on it) or press Ctrl+R. In both cases, the SQL statement is executed and the Results pane is updated to show all genres with an ID larger than 4. In your SQL pane, the query is now split over multiple lines to improve legibility. The SQL language enables you to spread your statements over multiple lines without the need for a line continuation character.

+   5. Now take a look at the Diagram pane — the top part of the dialog box in Figure 12-10 that shows your table diagram. In the Diagram pane you can check and uncheck column names to determine whether they end up in the query. Deselect the SortOrder column (don't accidentally change the check mark of the column in the Criteria pane instead). Note that it also gets removed from the Criteria pane and the SQL statement in the SQL pane (visible in Figure 12-11).