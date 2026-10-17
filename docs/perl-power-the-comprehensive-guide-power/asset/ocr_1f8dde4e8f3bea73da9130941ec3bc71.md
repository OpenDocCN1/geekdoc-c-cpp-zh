# # Passing Arrays to a Function

When you pass references to arrays to a function, each reference is assigned a separate index in
the function’s argument array. If you try to print the contents of the array argument, you find
only the address values representing the arrays. To access the contents of the arrays, you must
dereference the arrays. Listing13_08 explores passing and dereferencing references to three
arrays that contains the names of foods in different food groups. When the showData() func-
tion accesses the references, it dereferences them in reverse order.

```
```perl
#Listing13_08
#Pass Arrays to a function
#1 Define arrays
@Vegetables = ("Green beans", "Broccoli", "Brussels sprouts");
@Fruits = ("Apple", "Apricot", "Banana", "Cantaloupe", "Grapefruit");
@Legumes =("Kidney beans", "Lima beans", "Navy beans");
$RefToVegetables = \@Vegetables;
$RefToFruits = \@Fruits;
$RefToCookedLegumes = \@Legumes;
#Print the heading
makeTableHeading("Food Name", "");
#2 Pass the references to a function
showData($RefToVegetables, $RefToFruits, $RefToCookedLegumes);
#==============================================================
#3 ----- Definition of showData()------------------------------
#showData(array ref, array ref...)
sub showData{
	@ArrayInSub = (@_);
	$NumOfArrays = scalar(@ArrayInSub);
	$NL = "\n";
	#Traverse all the hash references -- in reverse order
	for($Itr = $NumOfArrays - 1; $Itr >= 0; $Itr--){
		print "$NL $NL Group $Itr $NL";
	#Retrieve each reference sequentially
		$Ref = $ArrayInSub[$Itr];
	#Retrieve the names of the foods and categories
```
```