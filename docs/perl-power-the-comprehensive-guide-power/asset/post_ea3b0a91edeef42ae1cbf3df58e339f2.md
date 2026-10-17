
## Functions That Return Values

```perl
sub convertAcreToHectare{
    #Use the return keyword to explicitly return the value
    return($_[0]/2.42);
    #or without return, the last active statement returns a value
    #($_[0]/2.42);
}
```

```perl
#9 --------- Definition of formatTableNote() ------------
#formatTableNote(string for table note)
sub formatTableNote{
    $NL = "\n";
    $CH = "-" x 52;
    #Join elements into a string
    #$TableNote =
    join("$NL ", $NL, $CH, @_);
    #or
    #return($TableNote) ;
}
```

At comment #1 in Listing12_05, you create a hash (%Footprints) that contains the names of ecological “footprints,” which are areas of the earth’s surface required to support given human consumption patterns. Following the definition of the data hash, you then create an array that provides information relating to the source of information in the %Footprints array.

At comment #2, you call the makeTableHeading() and provide four arguments to the function. The first furnishes the heading for the column that names the footprints. The second names the Acres column. The third names the Hectares column. For the last argument, you supply the name of the table, Ecological Footprints for the US.

The code associated with comment #3 (in the definition section of the program) reveals that you provide no return statement for the makeTableHeading() function. You require no return value from this function since it serves only to print the table heading, not to process information passed to other functions.

In the lines trailing comment #4, you call the makeTable() function and supply it with the %Footprint array as its lone argument. The argument array picks up the items in the hash, and at comment #5, in the definition section of the program, you assign the items from the argument array to the %LocalFP hash to restore them to their original key-value pairs. This then allows you to make use of the each repetition statement to print the items in the hash.

## The Explicit Use of return

At comment #6, which identifies lines inside the `makeTable()` definition block, you call a function that converts acreage to hectares (`convertAcreToHectare()`). To employ this function, you supply it with the lookup hash operation for `%LocalFP`. When you provide the key (`$Acres`) to the lookup operation, it provides the number of acres for the footprint the key identifies. The `convertAcreToHectare()` function performs its work and then returns a value to the `printf()` function through the `makeTable()` function, and as Figure 12.13 illustrates, you see the result displayed under the `Hectares` column heading.

You return this value explicitly (with the use of the `return` keyword). To return the value explicitly, in the definition of the `convertAcreToHectare()` function (see the lines following comment #7), you provide only one statement for the entire body of the function:

```
return($_[0]/2.42);
```

The `return` keyword accesses the result of the calculation and makes it available when the flow of the program reaches the end of the function and returns the value to the main flow of the program. If it is your task to maintain this code, the keyword enables you to recognize precisely how and where the function returns its value. When the `return` statement executes, it terminates the action of the function. Lines following it are not processed.

As a contrast, in the comment following the `return` statement, the program provides an example of how you can implicitly return the converted number.

```
#($_[0]/2.42);
```

Commenting out this line make no difference in the performance of the function because the function terminates with the execution of the `return` statement. However, it is good form to comment the line to show that it is not intended as a duplication of the `return` statement. Were you to comment out the `return` statement, this statement would take its place and implicitly return the result of the calculation.

On the other hand, as Figure 12.12 illustrates, if you reverse the order of the statements so that the explicit `return` statement follows the calculation, the `return` statement remains the last statement in the program. The flow of the program reaches the calculation, performs it, and without returning passes on to the following line, which contains the `return` statement. It then performs the calculation again and this time returns the result.

## The Implicit Use of return

The function call associated with comment #8 involves a cascading set of functions. The built-in Perl `print()` function takes as its argument the value that the `formatTableNote()` function returns. As an argument to the `formatTableNote()` function, you supply the `@FPIInfoSource` array. The purpose of the `formatTableNote()` function involves processing the array you furnish to it so that it can be printed as a single string.

At comment #9, in the section of the program dedicated to the definition of the `formatTableNote()` function, you employ the `join()` function to create a string using the elements of the array you have passed to the function. The function returns the string implicitly. Here is the code:

```
`$TableNote = join("\n ", $NL, $CH, @_);`
```

No `return` statement follows this statement. The performance of the `join()` operation stands as the last (uncommented) line of the function, and for this reason, as Figure 12.13 illustrates, the result of the `join` operation becomes the value the function returns. You can reduce the complexity of the code even further if you eliminate the assignment operation:

```
`join("\n ", $NL, $CH, @_);`
```

![](img/fd17b6cf7ddc9bc7e6f1529936c3ac84_343_0.png)

## CHAPTER 12 Functions

The function continues to perform its work because the `join()` function returns a string, and this action provides the value the `formatTableNote()` function supplies. Figure 12.13 illustrates the formatted string.

## Figure 12.13
You can return values implicitly or using the `return` keyword.

![](img/fd17b6cf7ddc9bc7e6f1529936c3ac84_344_0.png)

## Contexts and Returning Arrays and Hashes

As previous examples of using the argument array demonstrate, the context into which you introduce the returned value of a function determines how it is “cast.” In other words, if you use the returned value as a string, then it becomes a string. If you use it as a number, then it becomes a number. (If you cast a word as a number, the value of the word is 0.) This same relationship applies to hashes and arrays. Listing12_06 demonstrates how this works using an array that contains information relating to the way the biosphere dissipates solar radiation. The `sortRows()` function receives a hash as its argument. It processes the values in the hash and returns them as an array. The `displayTable()` function then displays the sorted data.

```
#Listing12_06
#Using contexts to process data in hashes and arrays
#1 set up table of media and percentages
%MediaOfDissipation = ("Reflected", 30,
       "Direct Conversion to Heat", 46,
       "Evaporation and Precipitation", 23,
       "Wind, Wave, Currents", 0.2,
       "Photosynthesis", 0.8
      );
```

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
