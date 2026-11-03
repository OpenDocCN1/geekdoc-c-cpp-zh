```
```cpp
// Fig. 21.5: fig21_05.cpp
// Contrasting input of a string via cin and cin.get.
#include <iostream>
using namespace std;

int main()
{
    // create two char arrays, each with 80 elements
    const int SIZE = 80;
    char buffer1[ SIZE ];
    char buffer2[ SIZE ];

    // use cin to input characters into buffer1
    cout << "Enter a sentence:" << endl;
    cin >> buffer1;

    // display buffer1 contents
    cout << "\nThe string read with cin was:" << endl
         << buffer1 << endl << endl;

    // use cin.get to input characters into buffer2
    cin.get( buffer2, SIZE );

    // display buffer2 contents
    cout << "The string read with cin.get was:" << endl
         << buffer2 << endl;
} // end main
```
```

Enter a sentence:
Contrasting string input with cin and cin.get

The string read with cin was:
Contrasting

The string read with cin.get was:
string input with cin and cin.get

Fig. 21.5 | Contrasting input of a string via cin and cin.get.

# Using Member Function getline

Member function getline operates similarly to the third version of the get member function and inserts a null character after the line in the built-in array of chars. The getline function removes the delimiter from the stream (i.e., reads the character and discards it), but does not store it in the character array. The program of Fig. 21.6 demonstrates the use of the getline member function to input a line of text (line 13).

```
```cpp
// Fig. 21.6: fig21_06.cpp
// Inputting characters using cin member function getline.
#include <iostream>
using namespace std;
```
```

Fig. 21.6 | Inputting characters using cin member function getline. (Part I of 2.)