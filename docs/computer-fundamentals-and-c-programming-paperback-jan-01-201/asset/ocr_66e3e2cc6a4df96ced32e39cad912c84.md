![](bbox=[0.249, 0.123, 0.743, 0.198])

**FIGURE 2.20** Copying a Cell

For copying a single cell to its adjacent location, use a shortcut: simply drag the handle at the lower-right corner of the copied cell to one or more adjacent cells (Fig. 2.20). A single value is thus copied to multiple cells.

When copying a range of such “simple” cells, you need to specify a single cell at the destination that signifies the top-left corner of the copied cells. The shortcut technique referred to previously applies but numbers need to be treated carefully. For instance, a row of three numbers can be dragged vertically but not horizontally. A converse reasoning applies to a column of numbers. If you drag a row of numeric cells horizontally, Excel thinks you are trying to complete a sequence and it fills up the blank cells with other values—not the copied ones.

**Copying Expressions and Formulas** Excel supports *Paste Special* that takes care of cell-reference and formula-related issues (Fig. 2.21). Two features should be noted. First, you can create a *link* between two cells. For instance, you may like to view the contents of a distant cell, say J200, at the top of the worksheet, say A20. Copy the cell J200 in the usual manner, but paste it at A20 using *Paste Link* from the *Paste Special* dialog box. J200 is now linked to A20, which means that changing J200 also changes A20.

The other feature relates to copying a formula. Consider that you have three columns of numbers and one of them has been summed with the SUM formula (Fig. 2.22). When you copy this cell

![](bbox=[0.268, 0.598, 0.708, 0.9])

**FIGURE 2.21** Paste Special Dialog Box