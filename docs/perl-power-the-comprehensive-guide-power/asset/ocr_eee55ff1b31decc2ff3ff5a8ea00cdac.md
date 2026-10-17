# # Contexts and Returning Arrays and Hashes

```
@InfoSource = ("Source: Eugene P. Odum, Ecology: A Bridge Between",
"Science and Society. Sunderland, MA: Sinauer Associates,",
"Inc., Publishers, p. 86");

#2 Pass arguments for the table heading - print heading
makeTableHeading("Medium ",
"\% Solar Radiation",
"Biospheric Dissipation of Heat");

#3 Pass the hash to a function that orders its elements
# and returns an array (see #4). Assign the array...
@SortedMedia = sortRows(%MediaOfDissipation);

#5 Pass the array to a function that prints the table rows
# (see #6)
printTable(@SortedMedia);

#7 Print the note for the table
print(printTableNote(@InfoSource));

############################################################
#-------- Definition of makeTableHeading() --------
#makeTableHeading(col head 1, col head 2, table title)
sub makeTableHeading{
#4 Formatting elements for the table
$NL = "\n ";
$DC = sprintf("%c", 254); #cast using sprintf to make a special character
$TW = 52; #Table width
$DL = sprintf( "%60s", $NL . $DC x $TW); #top and bottom lines
$COLAHEAD = $_[0];
$COLBHEAD = $_[1];
print "$NL $_[2]\n";
printf("$DL $NL");
printf("$NL %-30s %-10s $NL ", $COLAHEAD , $COLBHEAD);
printf("$DL $NL" );
}
```