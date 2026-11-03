3 Then, create two variables of the structure-defined data type, initializing both members of one variable
Point top = { 15 , 24 } ;
Point btm ;

4 Next, add a main function that initializes both members of the other variable of the structure-defined data type
int main()
{
    btm.x = 5 ;
    btm.y = 8 ;
}

5 Now, output the coordinates of both points
printf( "\nTop x: %d, y: %d\n" , top.x , top.y ) ;
printf( "Bottom x: %d, y: %d\n" , btm.x , btm.y ) ;

6 Before the main function block, insert a second structure defining a data type with two nested structure members
typedef struct
{
    Point a ;
    Point b ;
} Box ;

7 Next, declare a variable of the second structure-defined data type, initializing all its members
Box rect = { 6 , 12 , 30 , 20 } ;

8 Back in the main function block, output the coordinates of all points contained in the nested structure members
printf( "\nPoint a x: %d" , rect.a.x ) ;
printf( "\nPoint a y: %d" , rect.a.y ) ;
printf( "\nPoint b x: %d" , rect.b.x ) ;
printf( "\nPoint b y: %d\n" , rect.b.y ) ;

9 At the end of the main function block, return a zero integer value, as required by the function declaration
return 0 ;

10 Save the program file, then compile and execute the program to see the values stored in structure members