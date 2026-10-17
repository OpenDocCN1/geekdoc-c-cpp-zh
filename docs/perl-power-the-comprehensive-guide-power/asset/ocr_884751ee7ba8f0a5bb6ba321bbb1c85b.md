# # Figure 5.10 Specifiers and flags allow you to create table columns.

![](bbox=[0.323, 0.107, 0.884, 0.403])

numbers that must possess a uniform number of characters. Appending a plus sign to a number is at times handy, also.

```
```
#Listing05_10
# Variations
$PlRadiusOfEarth = 6357; #kilometers
$NL = "\n";
#1. #Prefixing a minus sign aligns the field to the left.
# No minus sign renders right justification.
printf ("%-1s %-10s %1s", "1|", "="x10, "|1");
print $NL;
#2. Append a period after the field width specifier and
# define the number of visible decimal places
# The field width is 9; the decimal places is 3
printf ("|%9.3f|", 123.1234567);
print $NL;
#3. Prefix a plus sign to show the sign
printf "%-20s %+15.2f","Polar radius of earth (km)", $PlRadiusOfEarth;
```
```

Figure 5.11 illustrates the output of Listing05\_10.