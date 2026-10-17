```
#2 Create a comma-delimited string
$PurchaseShipmentNotification = \
    join(",", (
    $CustomerEMailAddress,
    "Abe Washington", #literal string
    $Date));
print "\nCustomer Notice: " .
    $PurchaseShipmentNotification . $NL;
```

In the lines trailing #1 in Listing04_15, you use the same scalars used before in Listing04_14.
You add a scalar to hold the escape sequence for a new line. Then at comment #2 you call the
join() function. The first argument consists of a string. In this case the string contains a comma
followed by a space.

The second argument provides a list of items enclosed in parentheses. Within the parentheses,
you use two of the scalars defined previously. For purposes of demonstration, you add one lit-
eral string holding a name. To join the items into a single string, you assign the result of the
join() function (the return value) to a scalar, $PurchaseShipmentNotification.
You then print the contents of the scalar. Figure 4.22 illustrates the output of Listing04_15.

![](bbox=[0.16, 0.494, 0.929, 0.589])

# Creating the Notification with the join() Function

Given the discussion that the previous section provides, you can make use of the join()
function as an alternative approach to creating the customer notification shown in Figure 4.21.
Listing04_16 shows how this can happen.

```
#Listing04_16
#Using join to create a concatenated string

#1 Simulation of a record in a database
$NameOfCustomer = "Abe Washington";
$NameOfProduct = "Razor Might Version 4";
$CustomerEMailAddress = 'abeWash@my.com'; #single quotes for @ operator
$OrderNumber = "ASGM000456A7";
```