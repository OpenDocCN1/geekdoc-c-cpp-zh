```
while ( i < 5 )
{
    //Display num [ i ]
    cout << "num[" << i << "]" << num [ i ] << endl
    ;
    //Increment i
    i++;
}
```

Here is another example where in a *for* loop is used to fill an array with values from 1 to 10:

```
//Declare integer array
int x [ 10 ];
//For loop to run from 0 to 9
for ( int j = 0 ; j < 10 ; j ++ )
{
    //Fill array x
    x [ j ] = j + 1 ;
}
```

Let us write a C++ program which calculates the sum and average of 5 elements of a float array. These 5 elements will be entered by the user.

```
#include <iostream>

using namespace std;

int main()
{
    float values [ ], avg ;
    int i, sum ;
    cout << endl << endl
         << "Enter the number of elements" << endl ;
    for ( i = 0 ; i < 5 ; i++ )
    {
        cout << endl << "Enter value at index " << i
             << " : ";
        cin >> values [i];
```