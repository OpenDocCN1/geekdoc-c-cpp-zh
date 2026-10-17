# More on Implicit Assignment

The list function combined with the dot operators allows you to initialize arrays in a number of ways. Listing06_05 explores a few of the approaches.

```
#Listing06_05
#1 Numbers
@ArrayNum = (1..8);
print "\n ArrayE: @ArrayNum \n";

#2. Letters
@ArrayLet = ('f' .. 'm');
print "\n ArrayE: @ArrayLet \n";
#3. Expressions
@ArrayExpr = ('ab' .. 'am');
print "\n ArrayE: @ArrayExpr \n\n";

#5 Inventory and other numbers
@InventoryNumbers = (A0001111 .. A0009999);

print "\n A few numbers from the inventory list: \n";
for($Itr = 0; $Itr < 10; $Itr++){
    print "\n " . $Itr . " . " $InventoryNumbers[$Itr]";
}
```

The use of the list function in Listing06_05 illustrates numbers, letters, and expressions. As Figure 6.6 shows, you can create an extensive list of sequential numbers and then print them using a for statement. To access the inventory numbers, you can access the elements with a procedure similar to the one used in Listing06_05.

![](bbox=[0.392, 0.699, 0.823, 0.88])