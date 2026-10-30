# FIGURE 7.8

The main Link Spreadsheet Wizard screen.

![](bbox=[0.155, 0.22, 0.855, 0.595])

# Linking to HTML files

Linking to data contained in HTML documents is not covered in detail in this book because of the rather severe limitations imposed by Access on this process. For example, Access is unable to retrieve data from an arbitrary HTML file. The data must be presented as an HTML table, in a row-and-column format, and the data has to be relatively clean (absent any unusual data or mix of data, such as text, image, and numeric data combined within a single HTML table).

You're likely to encounter problems if more than one HTML table appears on the page or if the data is presented in a hierarchical fashion (parent and child data).

> Tip
> Linking to arbitrary HTML documents is hit or miss at best. You're much better off linking to an HTML document specifically prepared as a data source for your Access application than trying to work with arbitrary HTML files. If someone is going to the trouble of creating specialized HTML documents to be used as Access data sources, producing comma-separated values (CSV) or fixed-width text files is probably a better choice than HTML. CSV files, where the fields in each row are separated by commas, are commonly used for moving data from one application to another. CSV and fixed-width file types are discussed in the next section.