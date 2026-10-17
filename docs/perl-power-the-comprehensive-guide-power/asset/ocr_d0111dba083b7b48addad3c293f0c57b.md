# CHAPTER 5 } Scalars and Formatting

After defining the values of two identifiers at the start of Listing05_12, you then proceed at comment #2 to set up two scalars to hold formatting strings for use as arguments in the `printf()` function. This approach to formatting substantially reduces the complexity of arguments and provides a particularly effective approach to escaping the need to repeatedly code and debug formatting tags and specifiers. If you assign the specifiers as characters (using single quotes), the `sprintf()` and other functions can read them without errors.

Following the creation of the formatting scalars in the lines trailing comment #3, you create two rows for a table using the `sprintf()` function. When you create these rows, you assign the resulting strings to scalars ($RowA and $RowB). This work completed, you then use the `join()` function (explained in Chapter 4) to create a single scalar ($AstroTable) that contains the information for rows. When you employ the `join()` function, the first argument delimits the table you create using the $\NL identifier, which stores a new line escape sequence. This work accomplished, you call the `print()` function to print the table. The scalar $AstroTable is the sole argument. Figure 5.14 illustrates the output of Listing05_12.

![](bbox=[0.355, 0.425, 0.86, 0.487])

**Figure 5.14**  
Use of the `sprintf()` function allows you to create the rows of a table in a componential manner.

# Reworking the Table

When you use the `sprintf()` function in conjunction with formatting identifiers and concatenation, calling the `join()` function allows you to create a table that features a great deal of formatting detail and yet requires a minimum of redundant detail work—far less, in any event, than has been necessary in some of the previous coding efforts shown in this book. Listing05_13 represents a number of such labor-saving devices.

```
```text
#Listing05_13
#1 Define the data for the table
$P1RadiusOfEarth = 6357;
$PROEText = "Polar radius of earth (km)";
$EqRadiusOfEarth = 6378;
$EROEText = "Equatorial radius of earth (km)";
$EarthToMoon = 3.84401e6;
$EtMText = "Distance from Earth to Moon(km)";
$EarthToSun = 149597870.7;
$EtSText = "Distance from Earth to Sun (km)";
```
```