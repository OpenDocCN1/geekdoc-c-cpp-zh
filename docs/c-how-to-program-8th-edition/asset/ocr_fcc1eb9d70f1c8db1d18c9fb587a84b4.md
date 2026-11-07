```
```cpp
// Fig. F.3: figF_03.cpp
// Using command-line arguments
#include <iostream>
#include <fstream>
using namespace std;

int main( int argc, char *argv[] )
{
    // check number of command-line arguments
    if ( argc != 3 )
        cout << "Usage: copyFile infile_name outfile_name" << endl;
    else
    {
        ifstream inFile( argv[1], ios::in );

        // input file could not be opened
        if ( !inFile )
        {
            cout << argv[1] << " could not be opened" << endl;
            return -1;
        } // end if

        ofstream outFile( argv[2], ios::out );

        // output file could not be opened
        if ( !outFile )
        {
            cout << argv[2] << " could not be opened" << endl;
            inFile.close();
            return -2;
        } // end if

        char c = inFile.get(); // read first character

        while ( inFile )
        {
            outFile.put( c );  // output character
            c = inFile.get();  // read next character
        } // end while
    } // end else
} // end main
```
```

**Fig. F.3** Using command-line arguments.

This command line indicates that file input is to be copied to file output. When the program executes, if argc is not 3 (copyFile counts as one of the arguments), the program prints an error message (line 11). Otherwise, argv contains the strings "copyFile", "input" and "output". The second and third arguments on the command line are used as file names by the program. The files are opened by creating ifstream object inFile and ofstream object outFile (lines 14 and 23). If both files are opened successfully, characters are read from file input with member function get and written to file output with member function put until the end-of-file indicator for file input is set (lines 35–39). Then the program terminates. The result is an exact copy of file input. Note that not all computer