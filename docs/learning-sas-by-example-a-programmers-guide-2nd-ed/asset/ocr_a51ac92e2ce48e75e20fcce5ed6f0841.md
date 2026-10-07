# Chapter 22: Using Advanced Features of User-Defined Formats and Informs 385

# Program 22.8: Using Formats and Informs to Perform a Table Lookup

```
proc format;
  value NameLookup
122 = 'Salt'
188 = 'Sugar'
101 = 'Cereal'
755 = 'Eggs'
  other = ' ';
invalue PriceLookup
'Salt' = 3.76
'Sugar' = 6.99
'Cereal' = 5.97
'Eggs' = 2.65
  other = .;

run;

data Grocery;
  input ItemNumber @@;
  Name = put(ItemNumber,NameLookup);
  Price = input(Price,PriceLookup);
datalines;
101 755 122 189 755
;
```

A user-defined format is used, along with a PUT function, to retrieve a product name from the item number. An informat relating product names and prices, is used with an INPUT function to retrieve the price. An informat used for the price lookup because the INPUT function can return a numeric value. Remember that the PUT function always returns a character value. (If you used a format, you would have to perform a character-to-numeric conversion to obtain a numeric value for the price.)

Both the format and informat use the keyword OTHER to assign a missing value to an invalid item code. A listing of data set Grocery follows:

# Figure 22.7: Listing of Data Set Grocery

# Listing of Data Set Grocery

| ItemNumber | Name | Price |
|---|---|--|
| 101 | Cereal | 5.97 |
| 755 | Eggs | 2.65 |
| 122 | Salt | 3.76 |
| 188 | Sugar | 4.99 |
| 999 | | - |
| 755 | Eggs | 2.65 |