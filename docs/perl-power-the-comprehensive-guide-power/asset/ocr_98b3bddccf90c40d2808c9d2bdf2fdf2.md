# CHAPTER 4 **}** Print Functions

```
```php
$ProcessingNumber = "GH09824AA345-202029";
$Date = "12/12/06";
$PurchaseShipmentNotification = "";
$NL = "\n"; #Create a scalar new line

#2 A standard shipment notification form
#The entire report is created through arguments
# to one call to the join function
$PurchaseShipmentNotification =
    join("", (
                 $NL,
        $CustomerEMailAddress,                         $NL,
        $OrderNumber,                                  $NL,
        $Date,                                         $NL,
        "Dear ", $NameOfCustomer,                     $NL,
        "Thank you for your purchase of",              $NL,
        $NameOfProduct, ". Your shipping ",           $NL,
        "order is being processed. Your ",            $NL,
        "processing number is",                       $NL,
        $ProcessingNumber,                             $NL,
        "Respectfully,",                              $NL,
        "Customer Service",                           $NL));
print "\nCustomer Notification",                      $NL
      . $PurchaseShipmentNotification .             $NL;
```
```

In the lines associated with comment #1 in Listing04_16, you set up the same set of scalar variables you set up previously (in Listing04_14). In this case, you make one addition, the declaration of a scalar to hold the escape sequence for a new line. At comment #2, you proceed to create the string that holds the text of the message ($PurchaseShipmentNotification).

The first argument of the join() function consists of an empty string. You employ an empty string as the first argument because you need no delimiter between the items you concatenate. You then proceed in the second argument to set up a table to attend to the contents of your notification. Any number of approaches might be used to set up the notification. Placing the contents on the left side and the new line scalar variable on the right allows you to more easily discern the items in the report and its layout.