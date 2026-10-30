Clicking a column in the Total row transforms the datasheet cell to a drop-down list. The items in the drop-down list are specific to the column’s data type. For example, in text columns, the drop-down list shows only None and Count, while a numeric column contains a full complement of totals calculations (Sum, Average, Count, and so on). Date/Time columns include None, Average, Count, Minimum, and Maximum.

The Totals calculation you choose is dynamic. As you change data in the datasheet or underlying table, the calculation results displayed in the Total row are automatically updated after a very short delay. Recalculating a lot of totals extracts a small performance penalty, so you might want to hide the Total row when you aren’t using it.

The Totals options you choose for the columns in a datasheet persist. If you close the datasheet and re-open it, the Total row is still there.

To remove the Total row, open the datasheet and click the Totals button in the Records group on the Ribbon. Here’s one interesting behavior of the Total row: if you choose to remove it, you can restore it later (by clicking the Totals button again). The row is restored to its original setting.

# Printing Records

You can print all the records in your datasheet in a simple row-and-column layout. In Chapter 20, you learn to produce formatted reports. For now, the simplest way to print is to click File ➜ Print and choose one of the Print options as shown in Figure 5.24.

If you choose Print, and not Quick Print or Print Preview, Access shows the Print dialog box. From the Print dialog box, customize your printout by selecting from several options:

+   - **Print Range:** Prints the entire datasheet or only selected pages or records
+   - **Copies:** Determines the number of copies to be printed
+   - **Collate:** Determines whether multiple copies are collated

You can also change the printer, click the Properties button, and set options for the selected printer. The Setup button allows you to set margins and print headings.

The printout reflects all layout options that are in effect when the datasheet is printed. Hidden columns don’t print. Gridlines print only if the cell gridline properties are on. The printout also reflects the specified row height and column width.

Only so many columns and rows can fit on a page; the printout takes up as many pages as required to print all the data. Access breaks up the printout as necessary to fit on each page. For example, the tblProducts printout might be nine pages—three pages across are needed to print all the fields in tblProducts, and all the records require three pages in length. The records of tblContacts might need four pages in length. The number of pages depends on your layout and your printer.