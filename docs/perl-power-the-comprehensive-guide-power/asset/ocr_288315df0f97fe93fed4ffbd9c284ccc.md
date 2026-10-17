# # CHAPTER 12 Functions

```
###############################################################################
#3 --------- Definition of makeTableHeading() ------------
#makeTableHeading(col head 1, col head 2, table title)
sub makeTableHeading(){
	#4 Formatting elements for the table
	$NL = "\n ";
	$DC = sprintf("%c", 254); #cast using sprintf to make a special character
	$TW = 52; #Table width
	$DL = sprintf( "%60s", $NL . $DC x $TW); #top and bottom lines
	$COLAHEAD = $_[0];
	$COLBHEAD = $_[1];
	$COLCHEAD = $_[2];
	print "$NL $_[3] $NL";
	printf("$DL $NL");
	printf("$NL %-30s %-10s %-10s $NL ", $COLAHEAD , $COLBHEAD, $COLCHEAD );
	printf("$DL $NL" );
}
```

```
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
```

```
#7 --------- Definition of convertAcreToHectare() ------------
#convertAcreToHectare(hash for table)
```