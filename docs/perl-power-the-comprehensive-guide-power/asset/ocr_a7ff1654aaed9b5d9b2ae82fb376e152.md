# # CHAPTER 13 References

```
foreach $Name (@$Ref) {
    printf("$NL %-25s", $Name,)
    }#end foreach
    }#end for
}#end of showData()
#-------- Definition of makeTableHeading() --------
#makeTableHeading(col head 1, col head 2)
sub makeTableHeading{
    $NL = "\n ";
    $DC = sprintf("%s", "-");
    $TW = 50;
    $DL = sprintf("%55s", $NL . $DC x $TW); #top and bottom lines
    $COLAHEAD = $_[0];
    $COLBHEAD = $_[1];
    printf("$NL $DL $NL %-25s %-25s $DL ", $COLAHEAD , $COLBHEAD);
}
```

In the lines trailing comment #1 in Listing13_08, you first define three arrays that name foods from the vegetable, fruit, and legume groups. You then create references to these arrays using the reference operator (\\ ) and assign the references to scalars ($RefToVegetables, $RefToFruits, and $RefToCookedLegumes). You then proceed to set up the printing of a table to display the contents of the arrays. To accomplish this, in the line preceding comment #2, you call the makeTableHeading() function. This takes only one argument, Food Name.

Trailing comment #2, you call the showData() function. The function accepts three arguments, the references to the three arrays you defined previously. In the lines associated with comment #3, you define the function.

Your first task as you define the function involves assigning the contents of the argument array to a local array (@ArrayInSub). You then call the scalar() function to establish the number of elements the array contains and assign this number to a scalar identifier, $NumOfArrays. This identifier then becomes the initializing value for the counter of a for repetition statement ($Itr). When you initialize the counter using $NumOfArrays, you set the total number of references @ArrayInSub contains, so the operation of the repetition statement becomes one of decrementing from this number.

With the for block, you first print a line using the value in $Itr to identify the number of the group. The numbers in this case, as Figure 13.9 shows, begin with 2. With each iteration of the

348 *** TEAM LinG