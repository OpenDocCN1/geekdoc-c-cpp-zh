Figure 14-18 shows the output produced when the application is run. The form and the DataGridView control were enlarged using the windows resizing handles. The DataGridView was moved to the top-left corner of the form and the DataGridView control's Dock in Parent Container property was set. The Dock in Parent Container property is accessible from the smart tag on the top-right corner of the control.

![](bbox=[0.18, 0.33, 0.82, 0.7])

FIGURE 14-18 Example using Configuration Tools output

Values were not stored in alphabetical order by last name in the database. The DataGridView control provides the additional functionality of allowing columns to be sorted. The records shown in Figure 14-18 are sorted in ascending order by the last name. Clicking on the column heading for the last name refreshed the display, sorting the records by last name. A second click would rearrange the records in descending order by last name. The sorting capability is available for all of the columns.

# FORMATTING DATAGRIDVIEW CELLS

As noted earlier, when you select Edit Columns from the smart tag on the DataViewControl, the Bound Columns Properties window is displayed for individual columns. As shown in Figure 14-19, the appearance of the column can be formatted by selecting the first listed property, DefaultCellStyle. A CellStyle Builder is opened when you click this property. As shown in the middle window in Figure 14-19, the colors, font, alignment, and format for the cell are set using these properties.