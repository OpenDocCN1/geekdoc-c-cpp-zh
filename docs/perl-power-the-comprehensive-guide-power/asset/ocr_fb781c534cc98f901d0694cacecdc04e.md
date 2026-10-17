# Using the pop() Function

function reverses the order of keys in an array so that as you pop them, you see them in ascending order.

To accent the example, Listing08_06 makes use of the melting temperatures of chemical elements. As many chemists can relate, in 1742 Anders Celsius figured out how to convert degrees Celsius into degrees Fahrenheit. The formula that he presented reads as follows:

```
Fahrenheit = 9/5(Celsius) + 32
```

You can fold this formula into a program to add a column to an output table that shows the Fahrenheit values for the melting points of selective elements (see Figure 8.7). In the process, you can check your program for sanity by using the Celsius temperature at which water boils (100). On the Fahrenheit scale, water boils at 212 degrees.

```
#Listing08_06
# 1 Formatting elements for the table
$NL = "\n ";
$DC = "=";                  #character for top and bottom lines of table
$TW = 55;                   #Table width
$DL = sprintf( "%55s", $NL . $DC x $TW); #top and bottom lines
$COLAHEAD = "Element";
$COLBHEAD = "Celsius";
$COLCHEAD = "Fahrenheit";

#2 Set up the data using an implicit hash
%ElementsCelmEltingPts = ( (Water), 100,
                           Aluminum, 659, Carbon , 3600,
                           Chromium, 1615, Copper, 1083,
                           Gold, 1946, Hydrogen, -259,
                           Iron, 1530, Lead, 327,
                           Magnesium ,670, Manganese, 1260,
                           Nickel, 1452, Phosphorous, 44,
                           Silicon, 1420, Silver, 961,
                           Tin, 232, Titanium, 1795,
                           Tungsten, 3000, Zinc, 419);

#3 Print the table
printf("$DL");
printf("\n %-25s %-15s %-15s", $COLAHEAD, $COLBHEAD, $COLCHEAD);
printf("$DL");
```