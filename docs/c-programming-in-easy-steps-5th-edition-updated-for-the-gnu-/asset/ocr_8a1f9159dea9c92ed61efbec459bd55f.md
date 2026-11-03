![](bbox=[0.27, 0.1, 0.75, 0.16])

4 Now, test that both files were successfully opened
if( ( nums_ptr != NULL ) && ( hint_ptr != NULL ) )
{
}

5 In the if block, scan the integers from the file into the elements of the integer array
for( i = 0 ; !feof( nums_ptr ) ; i++ )
{
    fscanf( nums_ptr , "%d" , &nums[i] );
}

6 Next, in the if block, output the array element values
fprintf( stdout , "\nTotal numbers found: %d\n" , i );
for( j=0 ; j<i ; j++ ) { fprintf( stdout , "%d " , nums[j] ); }

7 Now, write the array element values into a file
fprintf( hint_ptr , "fscanf and fprintf are flexible\n" );
for( j=0 ; j<i ; j++ ) { fprintf( hint_ptr , "%d " , nums[j] ); }

8 Finally, in the if block, close both files upon completion
fclose( nums_ptr );
fclose( hint_ptr );

9 Add an alternative message for if the attempt should fail
else
{
    fprintf( stdout , "Unable to open a file\n" ); return 1 ;
}

10 Save the program file, then compile and execute the program to open a file then output and write its contents

![](bbox=[0.27, 0.78, 0.75, 0.9])