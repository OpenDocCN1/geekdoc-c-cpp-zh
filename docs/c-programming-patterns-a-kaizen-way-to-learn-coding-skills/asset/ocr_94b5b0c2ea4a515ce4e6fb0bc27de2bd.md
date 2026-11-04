```
// Column level Repetitive Action :
for ( int col = 0; * ( charPtr + col ) != '\0'; col++ ) {
    // filling array using '*' char at specific positions.
    
    if ( col == 0 ) {
        * ( charPtr + midIndex ) = '*';
    } else if ( col < totalRows ) {
        count = count + 1;
        * ( charPtr + midIndex - count ) = '*';
        * ( charPtr + midIndex + count ) = '*';
    } else {
        // for second-half portion
        * ( charPtr + midIndex - count ) = ' ';
        * ( charPtr + midIndex + count ) = ' ';
        count = count - 1;
    }
}

    // Print string and move cursor to the next row
    printf( "%s\n", charPtr );
}

    // freeing the allocated memory
    free( charPtr );
    printf( "Memory freed successfully.\n\n" );
}
```

# Output

Enter number of rows : 5
*
***
*****
*******
*********
***********
*************
***************
*************
***********
*********
*******
*****
***
*
Memory freed successfully.

Enter number of rows : 7
*
***
*****
*******
*********
***********
*************
***************
*****************
*******************
*******************
*****************
***************
*************
***********
*********
*******
*****
***
*
Memory freed successfully.