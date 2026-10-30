# Part II: Understanding Access Tables

Excel worksheets. You can change field names, specify a primary key, and save the import for future use. Save the imported text file with a descriptive Access table name. Access creates the new table, using the text file’s name by default. The new table appears in the Navigation pane.

> Tip
> To specify a field containing no data in a delimited file, leave no characters between the commas (not even a space character). An empty field at the end of a row is indicated by a comma at the end of the line.

# Fixed-width text files

Fixed-width text files also place each record on a separate line. However, each field has the same number of characters for every record (the character counts are fixed, thus the name). If a field has fewer characters than its fixed width, spaces are added to the end until it has the proper number of characters. Figure 6.13 shows an example of a fixed-width file. Even though the first column only contains one character, spaces are added so that the second column starts in the same place for every record.

# FIGURE 6.13

A typical fixed-width text file.

![](bbox=[0.22, 0.72, 0.78, 0.88])

Notice that the fields in a fixed-width text file are not separated by delimiters. Instead, they start at exactly the same position in each record, and each record has exactly the same length.

Text values, such as first and last names, are not surrounded by quotation marks. Because there are no column delimiters, there’s no chance that an illegal character can occur in a field, which would require the field to be text qualified. Anything within a field’s position in a row is considered that field’s data.