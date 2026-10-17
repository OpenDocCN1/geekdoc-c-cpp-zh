
## Chapter 12 Functions

In the definition of the function shown with trailing comment #5, in the definition section of the program, you make use of the implicit form of the argument array to access the items in the @GreenhouseGasses array. This use appears in the argument following the foreach repetition statement. It allows you to print the items in the array in table rows. Here are the lines:

```perl
foreach $Gas (@_) { #lines left out
```

You do not require the scalar form of the array in this instance because you have no need to access items specifically, as is the case when you process the column heads and the table title in the makeTableHeading() function. Here, by traversing the array and printing each item successively, you fulfill the requirements set for the function.

You can use the scalar and implicit forms of the argument together or exclusively in any given function definition. Figure 12.10 shows the table that results from the use of the two approaches to passing the argument array.

**Figure 12.10** You can use the argument array directly without copying it locally.

![](img/fd17b6cf7ddc9bc7e6f1529936c3ac84_336_0.png)

### Passing a Hash as an Argument

When you pass a hash to a function, the argument array converts the hash into an array. To process the hash in the function definition, you must convert the items that the argument array provides back into a hash. You can accomplish this by assigning the argument array to a hash. Listing12_04 processes data that shows atmospheric increases in parts per million (PPM) of CO₂ over the past few centuries. The program involves passing a hash containing atmospheric data to a function. The function retrieves data from the argument array, converts it back into a hash, and then prints the data by year in tabular form using the lookup hash operation.

```perl
#Listing12_04
#Passing a hash to a function

#1 Set up data on CO2 in the atmosphere
%CO2Changes = ("1750", "180",
		"1970", "320",
		"1980", "330",
		"2000", "360",
		"2025", "450");

#2 Pass arguments for the table heading
makeTableHeading("Year",
		"CO2 Parts Per Million",
		"Rise In Atmospheric Carbon Dioxide");

#4 Pass the hash to a function
makeTable(%CO2Changes);

#==============================================================
#3
#-------- Definition of makeTableHeading() --------
#makeTableHeading(col head 1, col head 2, table title)
sub makeTableHeading{
	#4 Formatting elements for the table
	$NL = "\n ";
	$DC = sprintf("%c", 247); #cast using sprintf to make a special character
	$TW = 50; #Table width
	$DL = sprintf( "%50s", $NL . $DC x $TW); #top and bottom lines
	$COLAHEAD = $_[0];
	$COLBHEAD = $_[1];
	print "$NL $_[2] $NL";
	printf("$DL $NL");
	printf("$NL %-15s %-40s $NL ", $COLAHEAD , $COLBHEAD);
	printf("$DL $NL" );
}

#5-------- Definition of makeTable() --------
#makeTable(hash for table)
sub makeTable{
	$NL = "\n ";
	%LocalCO2 = @_;               #Assign argument array to hash
	@CO2Years = keys(%LocalCO2);  #extract keys for sorting
	@CO2Years = sort {$a<=>$b}(@CO2Years);  #perform the sort
	#Use the sorted years (array) to extract the values (hash)
	foreach $Year (@CO2Years){                       #access the argument array here
	    printf("$NL %-15s %-40s $NL", $Year, $LocalCO2{$Year});
	}
}
```

In the lines that comment #1 in Listing12_04 identifies, you set up a hash (%CO2Changes) that lists dates and CO₂ levels for the past few centuries. Immediately after defining the hash, at comment #2, you call the makeTableHeading() function and supply it with three arguments. As Figure 12.11 reveals, these name the table and supply Year and CO₂ Parts Per Million as the column headings.

In the lines associated with comment #4, you pass the %CO2Changes to the makeTable() function. You supply the hash to the function in its implicit form. In the lower part of the program, at comment #5, you retrieve the hash from the argument array by assigning it to a local hash identifier, %LocalCO2. Assignment automatically translates the items in the hash into key-value pairs.

Following the definition of the local hash, you use the keys() function to assign the years (keys) in the local hash to a local array (@CO2Years). In the line following the definition of this array, you sort the years using the numerical form of the Perl sort() function. You then proceed into a foreach repetition statement in which you employ the sorted years in @CO2Years to access the items in the %LocalCO2 hash. To accomplish this, you use the hash lookup operation. When you employ the sorted array to retrieve the values (CO₂ levels) from the hash, the years unfold in the table in ascending order. As Figure 12.11 reveals, it is also the case that the level of CO₂ grows with the passing years. Note that the data for 2025 is projected.

![](img/fd17b6cf7ddc9bc7e6f1529936c3ac84_338_0.png)

### Functions That Return Values

You can return values from functions in two ways. One way involves using the keyword `return` followed by the argument you want to return. The other approach is to allow the function to return the result of its last active statement. Listing12_05 works with the conversion of acres to hectares. Ecologists measure the ecological footprint of the human population in terms of the number of hectares needed to support consumption levels. Listing12_05 generates a table that shows figures for acres in one column and hectares in another. The definition and call to a function that converts acres to hectares demonstrate the use of the `return` keyword. On the other hand, the definition and call to a function that returns a string that serves to identify the source of the information the function contains demonstrate how you can implicitly return the results of the final statement in a function.

```perl
#Listing12_05
#Passing and returning a value
#1 Footprints for US in acres
   %Footprints = ("Fossil/Nuclear Power",  14.5,
      "Built-up Areas",     0.9,
      "Growing Crops",      3.7,
      "Grazing Animals",    0.8,
      "Harvesting Fish and Sea Food", 0.8);
#Source of information
@FPInfoSource = ("Source: M. Wackernagel, C. Monfreda, D. Deumling",
   "\"Ecological Footprint of Nations.\" November, 2002.",
   "Redefining Progress www.redefiningprogress.org.");
#2 Pass arguments for the table heading
makeTableHeading("Footprint Type",
   "Acres",
   "Hectares",
   "Ecological Footprints for the US");
#4 Pass the hash to a function
makeTable(%Footprints);
#8 Cascading functions: print calls to printTableNote
# See #9 - printTableNote returns implicitly
print(formatTableNote(@FPInfoSource));

###############################################################################
#3 --------- Definition of makeTableHeading() ------------
#makeTableHeading(col head 1, col head 2, col head 3, table title)
sub makeTableHeading(){
	#4 Formatting elements for the table
	$NL = "\n ";
	$DC = sprintf("%c", 254); #cast using sprintf to make a special character
	$TW = 52; #Table width
	$DL = sprintf( "%52s", $NL . $DC x $TW); #top and bottom lines
	$COLAHEAD = $_[0];
	$COLBHEAD = $_[1];
	$COLCHEAD = $_[2];
	print "$NL $_[3] $NL";
	printf("$DL $NL");
	printf("$NL %-30s %-10s %-10s $NL ", $COLAHEAD , $COLBHEAD, $COLCHEAD );
	printf("$DL $NL" );
}

#5 --------- Definition of makeTable() ------------
#makeTable(hash for table)
sub makeTable(){
	$NL = "\n ";
	%LocalFP = @_; #Assign argument array to hash
	@FPAcres = keys(%LocalFP); #extract keys for sorting
	#Use the sorted years (array) to extract the values (hash)
	foreach $Acres (@FPAcres){ #access the argument array here
		printf("$NL %-30s %-10.2f %-10.4f $NL ",
			$Acres,
			$LocalFP{$Acres},
			convertAcreToHectare($LocalFP{$Acres})
		);
	}#end foreach
}#end makeTable

#7 --------- Definition of convertAcreToHectare() ------------
#convertAcreToHectare(hash for table)
```
