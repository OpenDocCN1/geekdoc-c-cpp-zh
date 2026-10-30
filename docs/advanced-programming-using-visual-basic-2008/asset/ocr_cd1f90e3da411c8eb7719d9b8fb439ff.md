STEP 2: Increase the top margin to 1.0 inch. You also can increase the left and right margins if your printer is one of those that cannot print closer than one-third inch from the edge of the page. Click OK.

# Sort the Report

STEP 1: Right-click on the report design to display the context menu. Select *Report / Record Sort Expert*. Currently the report is sorted by the CategoryName field; we want to sort by product name within each category group.

STEP 2: Add Product.ProductName to the list. Notice the *Sort Direction* defaults to *Ascending*. Click OK.

STEP 3: Run your program again. This time the report should be sorted by product name within categories, with a larger top margin.

Look carefully at the column headings and data in the fields. Many are cut off and should be fixed. Stop the program and return to design view so you can further modify and beautify the report.

# Add a Calculated Field

STEP 1: Display and examine the Field Explorer (Figure 9.13). Notice that you can expand the nodes for the database fields to see which fields are included in the report or used in a formula. The selected fields appear with a check mark.

![](bbox=[0.285, 0.468, 0.497, 0.868])

> **Figure 9.13**
> 
> *The Field Explorer shows the fields that are included in the report and can be used to add new fields.*

STEP 2: Right-click on Formula Fields and select New from the context menu.

STEP 3: Enter ExtendedPrice for the formula name and click Use Editor. The Formula Workshop - Formula Editor opens to help you create a new formula (Figure 9.14).