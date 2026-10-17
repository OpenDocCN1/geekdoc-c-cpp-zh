to obtain the number of gem names the array contains. This value you assign to the `$Length` identifier.

After printing the table heading (see the lines associated with comment #4), you then proceed at comment #5 to create a repetition loop using the `until` statement. To accomplish this, you first create a control identifier (`$Count`), which you initialize to zero. Then you enter the `until` control condition. The conditional expression you create relates `$Count` to `$Length`, using the greater than relational operator. As long as `$Count` remains less than or equal to `$Length`, the loop continues to iterate.

Having entered the `until` block, you call the `printf()` function to create the table rows. To retrieve the names of the gems for the first column, you use `$Count` to access the indexes of the `@GemNames` array. As a second argument to `printf()`, to create the second table column, you employ the lookup hash operation. To access the data for this column, you again use the scalar form of the `@GemNames` array, this time with `$Count` incremented using the unary (incremental) operator. The gem name you retrieve from the array becomes the key you use to loop up the corresponding gem category. Figure 11.12 shows you the resulting table of gems and their categories.

![](bbox=[0.154, 0.472, 0.62, 0.633])

**Figure 11.12**  
The `until` statement iterates while a given condition proves false.

# The do...until Statement

The `do...until` control statement allows you to place your control expression at the end of the control block. In this way, the flow of your program can enter the block area without being tested, performing the statements within the block at least once. Statements in the block continue to execute as long as the control statement remains false. Listing11_07 explores the use of the `do...until` statement to create a table of minerals and brief descriptions of them.

```
#Listing11_07
#Using do...until
#1 Formatting elements for the table
$NL = "\n ";
```