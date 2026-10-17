```
```perl
#====================================================================
#------------- Definition of makeTableHeading() ------------
#makeTableHeading(col head 1, col head 2)
sub makeTableHeading{
    $NL = "\n ";
    $DC = sprintf("%s", "-");
    $TW = 50;
    $DL = sprintf( "%55s", $NL . $DC x $TW); #top and bottom lines
    $COLAHEAD = $_[0];
    $COLBHEAD = $_[1];
    printf("$NL $DL $NL %-25s %-25s $DL $NL", $COLAHEAD , $COLBHEAD);
}
```
```

In the lines associated with comments #1 and #2 in Listing13_05, you define an array (@Vegetables) and then define a reference for the array that you assign to a scalar ($RefToVegetables). You use the scalar() function to access the number of items in the array. To access the array, you dereference the scalar that stores the reference to the array (@$RefToVegetables).

At comment #3, you again employ a dereferencing strategy to access the items in the array (@$RefToVegetables). As is evident following Heading 1 in Figure 13.6, you can then use the dereferenced array in a foreach structure and retrieve items from it as though it were a regular array.

At comment #4, you dereference the array still again, and this time the result is that you can retrieve items from the array using their indexes. To accomplish this task, you create a scalar that you can use to traverse the array ($Count). You likewise employ the scalar, defined earlier, that stores the size of the array ($Size). Using a while repetition statement, you then traverse the indexes of the array and print them. The listing following Heading 2 in Figure 13.6 shows the results.

In the lines trailing comment #5, you make use of the pointer operator in conjunction with the index brackets ($RefToVegetables->[$Count++]). The pointer operator allows you to retrieve items directly from the array reference. Using the incremented values of the $Counter identifier to access the array items, you can print them without further ado because they do not themselves represent referenced values. Only the array container is referenced. You access the name of the vegetables through the referenced array. The list following Heading 3 in Figure 13.6 shows the output of this operation.