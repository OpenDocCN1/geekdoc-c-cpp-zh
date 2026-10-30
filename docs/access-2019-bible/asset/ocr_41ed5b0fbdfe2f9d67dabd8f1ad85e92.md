in the other database. Figure 6.29 shows that tblEmployees was successfully exported to a SQLite3 database.

# FIGURE 6.29

The Employees table has successfully exported to a SQLite3 database.

![](bbox=[0.18, 0.26, 0.86, 0.6])

# Exporting to Word

Access provides two ways to transfer data to Word: Export to Rich Text Format and Word Merge. Rich Text Format (RTF) is a plain text file with special characters that define the formatting. Exporting to RTF creates a document with an RTF extension, not a native Word document (though Word can read RTF, as can WordPad and many other text editors).

# Merging data into Word

The real power of exporting to Word is to use the data in Word Merge. With Word Merge, you can control where your data ends up in the Word document. This is useful for such tasks as sending letters, addressing envelopes, producing reports, and creating file folder labels.

To create file folder labels for each department in tblDepartments, follow these steps:

+   1. Open tblDepartments in Datasheet view.
+   2. Click the Word Merge button in the Export group on the External Data tab.
+   3. On the first screen of the Microsoft Word Mail Merge Wizard, shown in Figure 6.30, select Create a New Document and Then Link the Data to It, and click OK. Word opens to a new document and the Mail Merge task pane appears on the right.