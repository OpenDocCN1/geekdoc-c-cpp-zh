We will need a total of 3 loops – one outer loop to keep track of the lines, two inner loops to keep track of the number of spaces to be left and the number of stars to be printed. Here is the code:

```
```cpp
#include <iostream>
using namespace std;
int main ()
{
    int i, j, k, space = 5, star = 1 ;
    cout << endl << endl;

    // loop for no. of lines
    for (i = 1 ; i <= 5 ; i ++)
    {
        space -- ;
        star = ( 2 * i) - 1 ;
        j = 1 ;

        while ( j ++ < space )
        {
            // leave spaces "space" number of times
            cout << ' ' ;
        }
        k = 1 ;

        while ( k ++ < star )
        {
            // print star "star" number of times
            cout << '*' ;
        }
        cout << endl ;
    }
    cout << endl << endl ;
    return 0 ;
}
```
```

Output: