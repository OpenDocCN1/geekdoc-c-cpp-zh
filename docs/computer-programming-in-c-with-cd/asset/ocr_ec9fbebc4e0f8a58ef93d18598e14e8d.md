```
m = x; //Initializing both the number of rows and columns to be equal to
the
                    //number of elements in the square matrix in either the row or
                    column.
n = x;
init(); //Calling the function init() to initialize the elements of the
array
}

matrix::matrix(int x,int y) //Constructor Overloading, constructor to
                    initialize if the
                    //number of rows are not equal to the number of columns,
                    //i.e if the matrix is a rectangular matrix.
{
m = x;
n = y;
init(); //Calling the function init() to initialize the elements of the
array
}

void matrix::init()
{
int i,j;
for(i=1;i<=m;i++)
    for(j=1;j<=n;j++)
        a[i][j] = 0; //Initializing all the elements of that array to be equal to
zero.
}

void matrix::input() //Function to input the elements of the matrix
{
int i,j;
cout<<"\n enter the array elements one by one\n";
for(i=1;i<=m;i++) //Counter for the number of rows of the matrix
    for(j=1;j<=n;j++) //Counter for the number of columns of the matrix
        cin>>a[i][j];
}

void matrix::display() //Function to output the elements of the matrix
{
int i,j;
for(i=1;i<=m;i++) //Counter for the number of rows
{
        cout<<endl; //After every row is printed move to a new line
        for(j=1;j<=n;j++) //Counter for the number of columns
```