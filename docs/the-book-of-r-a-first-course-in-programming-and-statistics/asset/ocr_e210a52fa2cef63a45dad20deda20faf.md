machine. Use a delimiting character of ! and do not include any row names.
ii. Read the file back into your R workspace, naming the object q5.dframe.
b. In the contributed package car, there’s a data frame called Duncan, which provides historical data on perceived job prestige in 1950. Install the car package and access the Duncan data set and its help file. Then, do the following:
i. Write R code that will plot education on the x-axis and income on the y-axis, with both x- and y-axis limits fixed to be [0,100]. Provide appropriate axis labels. For jobs with a prestige value of less than or equal to 80, use a black o as the point character. For jobs with prestige greater than 80, use a blue ●.
ii. Add a legend explaining the difference between the two types of points and then save a 500 × 500 pixel .png file of the image.
c. Create a list called exer that contains the three data sets quakes, q5.dframe, and Duncan. Then, do the following:
i. Write the list object directly to disk, calling it Exercise8-1.txt. Briefly inspect the contents of the file in a text editor.
ii. Read Exercise8-1.txt back into your workspace; call the resulting object list.of.dataframes. Check that list.of.dataframes does indeed contain the three data frame objects.
d. In Section 7.4.3, you created a ggplot2 graphic of 20 observations displayed as the bottom image of Figure 7-11 on page 144. Use ggsave to save a copy of this plot as a .tiff file.

# Important Code in This Chapter

| Function/operator | Brief description | First occurrence |
|---|---|---|
| data | Load contributed data set | Section 8.1.2, p. 149 |
| read.table | Import table-format data file | Section 8.2.1, p. 151 |
| list.files | Print specific folder contents | Section 8.2.1, p. 151 |
| file.choose | Interactive file selection | Section 8.2.1, p. 152 |
| read.csv | Import comma-delimited file | Section 8.2.2, p. 153 |
| write.table | Write table-format file to disk | Section 8.3.1, p. 156 |
| jpeg, bmp, png, tiff | Write image/plot file to disk | Section 8.3.2, p. 157 |
| dev.off | Close file graphics device | Section 8.3.2, p. 157 |
| pdf, postscript | Write image/plot file to disk | Section 8.3.2, p. 158 |
| ggsave | Write ggplot2 plot file to disk | Section 8.3.2, p. 159 |
| dput | Write R object to file (ASCII) | Section 8.4, p. 160 |
| dget | Import ASCII object file | Section 8.4, p. 161 |