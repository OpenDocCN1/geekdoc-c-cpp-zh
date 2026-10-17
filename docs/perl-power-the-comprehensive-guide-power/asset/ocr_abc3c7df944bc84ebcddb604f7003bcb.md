# # CHAPTER 9 Extending Hash Applications

```
#4 Assign the elements to an array
@NElementNames = keys(%NewlandsElements);
#5 Use an inner foreach loop and a selection statement
#to retrieve the names of elements
	$Itr = 1;
	foreach $NEName (@NElementNames) {
		if(!defined($MendeleevElements{$NEName})) {
			printf("\n %-15s %-15s %-15s",
				$NEName,
				$NewlandsElements{$NEName},
				"Newlands");
		}
	}
system("pause");
```

To format the output table, at comment #1 you define several identifiers with information relative to formatting. At comment #2, you set up two hashes. The first hash contains data Mendeleev used. The second hash contains data Newlands used. At comment #3, you print the heading of the output table.

In the lines associated with comment #4, you assign the keys of the hash that contain the data Newlands used to an array, @NElementNames. With this array in place, you then proceed in the lines trailing comment #5 to employ a foreach control statement to traverse the items in the @NElementNames array. As you access the names of the elements, you temporarily assign them to the $NEName identifier.

After assigning the name of an element to the $NEName identifier, you can then use the identifier in the hash lookup operation, which you evaluate using the NOT form of the defined() function (!defined()). The purpose of this operation is to test for keys that are not defined in the hash that contains the data Mendeleev used (%MendeleevElements).

You test each of the elements Newlands used. Each time you find one that is not present in the Mendeleev data, you print it. In addition to the element name, you print the status associated with it. In each case, the status is “D.” You also print “Newlands”to confirm that the data was used only by Newlands. Figure 9.2 displays the output of Listing09_02.