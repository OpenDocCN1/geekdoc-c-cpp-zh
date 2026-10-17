# # Swapping

When you swap elements in an array, you improvise on the basic routine afforded by slicing. To effect a swap, you reassign an array to itself, and as you do so you employ indexes to define how you want to reorganize (or swap) the elements. Listing06_07 explores a basic swapping scenario:

```
#Listing06_07
#1 Create an array
@CanadianCities = ("Amos" , "Barrie" , "Battleford" ,
"Beauport", "Bonavista");
$Itr = 0;
print "\n Original order:\n ";
foreach $City (@CanadianCities){
print "\n ". $Itr++ . ". ". $City";
}
#2 Use swapping to rearrange the elements
@CanadianCities[0,3,2,1] = @CanadianCities[4,1,2,3];
#print results of swapping
$Itr = 0;
print "\n\n Rearranged order: \n";
foreach $City (@CanadianCities){
print "\n ". $Itr++ . ". ". $City";
}
```

At comment #1, you set up an array of Canadian cities and then print the array with an iterator so that you can see the order. Then at comment #2, you set up a swapping routine. The routine involves using the implicit (@) form of the array and multiple indexes between brackets to indicate the elements you want to swap. To make the swap, you assign the array back to itself.

![](bbox=[0.0742, 0.1094, 0.8281, 0.2266])