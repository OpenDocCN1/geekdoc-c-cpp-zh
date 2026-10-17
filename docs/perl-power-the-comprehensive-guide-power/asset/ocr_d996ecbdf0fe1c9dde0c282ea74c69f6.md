```
```r
printf("%-36s %20.0f $12s", $NL . "Distance to the farthest Galaxy",
       $FarthestGalaxy, $LY);
printf("%-36s %20.0f $12s", $NL . "Diameter of the Milky Way",
       $MilkyWayDiameter, $LY);
printf("%-36s %20.0f $12s", $NL . "Thickness of the Milky Way",
       $MilkyWayThickness, $LY);
printf("%-36s %20.0f $12s", $NL . "Number of stars in the Milky Way",
       $StarsInMilkyWay, "$LY");
print "$NL $NL $NL";
```
```

The code accompanying comment #1 in Listing05_09 defines a set of values for the table. With the code associated with comment #2, you begin working through the list of data to create the table using the `printf()` function. In each use of the `printf()` function you create three columns. The first column presents a string. For the string, you concatenate a scalar identifier containing a new line escape sequence with literal strings that introduce the astronomical data the table presents. Each use of the `print()` function creates a row in your table.

You set the field width for the first column of the table to be 36 characters wide, justified to the left, and of the string type. In this respect, all the rows are the same. You make the third column of the table consist of fields 12 characters wide and of the string type. You allow the default right justification to apply to these fields.

The middle or second column of the table sports three types of fields. The fields are all 20 characters wide, but in some cases they display decimal values. In other cases, they display float values. In one field you use the `e` specifier to force the number to display in scientific notation. This value pertains to the speed of light in kilometers. To show a comparison between scientific notation and a standard decimal number, you also use the `f` formatting specifier.

Figure 5.10 illustrates the appearance of the table. The conversion specifiers for the data you employ in the table considerably improve the appearance of the data over previous displays. The numbers show no decimal places when it does not seem reasonable to display them. On the other hand, they can be shown (in the instance of the distance to Proxima Centauri) when the decimal places make sense.

# Variations

Listing05_10 provides a few examples of common formatting operations. As previous sections have emphasized, you can use a minus sign to left justify a column. You can employ such capabilities in combination with type specifiers to create specific results, such as fillers. Such techniques can come in handy for creating headers. You can also prefix a zero to a specifier to fill a column with zeros. You might use this formatting procedure to generate inventory or other